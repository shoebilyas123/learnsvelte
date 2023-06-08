<script>
    import Card from "../UI/Card.svelte";
    import { feedbacks as FeedbackStore } from "../store";
    import Button from "./Button.svelte";
    import RatingSelect from "./RatingSelect.svelte";
    
    let text = '';
    let btnDisabled = true;
    let min = 10;
    let message = null;
    let rating = 10;
    let timeout = null;
    
    const handleRatingSelect = (event)=>{
        rating = event.detail;
    }

    const clearMessage = ()=>{
        timeout = setTimeout(()=>{
            message = "";
            return ()=>timeout = null;
        },2000)
    }

    const handleInput = ({target:{value}})=>{
        if(value.trim().length <= min){
            message = "Please enter at least 10 characters";
            btnDisabled = true;
        }else{
            text = value;
            btnDisabled = false;
            message = null;
        }
    }

    const handleSubmit = ()=>{
        if(text.trim().length <= min){
            message = "Please enter at least 10 characters";
            btnDisabled = true;
            return;
        }

        const newFeedback = {
            id: Math.random().toString(12),
            rating,
            text
        }

        FeedbackStore.update((currentFeedbacksList)=>{
            return [newFeedback, ...currentFeedbacksList];
        });

        text = '';
        rating = null;
        btnDisabled = true;
        message = "Thank you for your feedback!";
        clearMessage();
    }

</script>

<Card>
    <header>
        <h2>Feedback Form</h2>
    </header> 
    <form on:submit|preventDefault={handleSubmit}>
        <RatingSelect on:rating-select={handleRatingSelect}/>
        <div class="input-group">
            <input class="text" value={text} on:input={handleInput} placeholder="Tell us something that keeps you coming back"/>
            <Button style={"primary"} type="submit" disabled={btnDisabled}>Send</Button>
        </div>
    {#if message}
    <div class="message">{message}</div>
    {/if}
    </form>
</Card>

<style>
    header {
      max-width: 400px;
      margin: auto;
    }
  
    header h2 {
      font-size: 22px;
      font-weight: 600;
      text-align: center;
    }
  
    .input-group {
      display: flex;
      flex-direction: row;
      border: 1px solid #ccc;
      padding: 8px 10px;
      border-radius: 8px;
      margin-top: 15px;
    }
  
    input {
      flex-grow: 2;
      border: none;
      font-size: 16px;
    }
  
    input:focus {
      outline: none;
    }
  
    .message{
      padding-top: 10px;
      text-align: center;
      color: rebeccapurple;
    }
  </style>