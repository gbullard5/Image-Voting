<script>
import {carArray} from "../CreateArray";
let sortedCarArray = carArray;
let chosenCar = null;
const decrement = (car) => {
        if (car.count == 0){

         } else {
            car.count -= 1
        }
        return car;
    }

const sort = (carArray) => {
  carArray.sort((a,b)=> b.count-a.count);
  return carArray;
}

</script>
<h2>Top Rated</h2>
<main>
  
  {#each sortedCarArray.slice(0,3) as car}
  <div class="border">
  <section class="top">
    <div class="car">
      <h2>{car.name}</h2>
      <img class="thumbnail" src={car.thumbnail} on:click={()=> chosenCar = car}/>
    </div>
    <p>{car.caption}</p>
    <div class="buttons">
      <button on:click={()=> {car.count++; sortedCarArray = sort(carArray)}}>Upvote</button>
      <button on:click={() => {car = decrement(car); sortedCarArray = sort(carArray) } }>Downvote</button>
    </div>
  </section>
</div>
  {/each}
  </main>
  <h2 class="remaining">Remaining Photos</h2>
  <main>
  {#each sortedCarArray.slice(3,9) as car}
  <section>
    <div class="car">
      <h2>{car.name}</h2>
      <img class="thumbnail" src={car.thumbnail} on:click={()=> chosenCar = car}/>
    </div>
    <p>{car.caption}</p>
    <div class="buttons">
      <button on:click={()=> {car.count++; sortedCarArray = sort(carArray)}}>Upvote</button>
      <button on:click={() => {car = decrement(car); sortedCarArray = sort(carArray) } }>Downvote</button>
    </div>
  </section>
  {/each}
</main>

{#if chosenCar != null}
<div class="popup">
  <h2>{chosenCar.name}</h2>
  <img src={chosenCar.image} />
  <p>{chosenCar.caption}</p>
  <button on:click={()=> {chosenCar.count++; sortedCarArray = sort(carArray)}}>Upvote</button>
  <button on:click={() => {chosenCar = decrement(chosenCar); sortedCarArray = sort(carArray) } }>Downvote</button>
  <button on:click={()=> chosenCar = null}>Close</button>
</div>
{/if}


<style>
  main {
    display: grid;
    grid-template-columns: auto auto auto;
    gap: 1rem;
  }

  .popup{
    position:absolute;
    top: 10px;
    padding: 50px;
    background-color: lightyellow;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    border-radius: 15pt;
  }

  section {
    display: flex;
    height: 450px;
    flex-direction: column;
    align-items: center;
    position: relative;
    padding: 0.5rem;
    border-radius: 15pt;
    border: 1px solid;
    box-shadow: 4.0px 8.0px 8.0px rgb(0 0 0 / 0.38);
    background-color:lightgray;
  }

  .top{
    display: flex;
    height: 450px;
    flex-direction: column;
    align-items: center;
    position: relative;
    padding: 0.5rem;
    border-radius: 15pt;
    border: 1px solid;
    box-shadow: 4.0px 8.0px 8.0px rgb(0 0 0 / 0.38);
    background-color:goldenrod;
  }

  img{
    border-radius: 15pt;
  }

  .thumbnail{
    border-radius: 15pt;
    height: 250px;
    width: 400px;
  }
  button{
    background-color:aliceblue;
    
  }

  .remaining{
    margin: 40px;
    margin-top: 80px;
  }

</style>