// 代码生成时间: 2025-11-01 17:28:53
  // Define the store for options and votes
  import { writable } from 'svelte/store';

  const options = writable([
    { id: 1, text: 'Option 1', votes: 0 },
    { id: 2, text: 'Option 2', votes: 0 },
    { id: 3, text: 'Option 3', votes: 0 }
  ]);

  // Function to cast a vote for an option
  function castVote(optionId) {
    try {
      // Ensure option exists
      const option = options.update((currentOptions) => {
        return currentOptions.map((option) => {
          if (option.id === optionId) {
            return { ...option, votes: option.votes + 1 };
          }
          return option;
        });
      });

      // Error handling if option is not found
      if (option && option.votes === 0) {
        throw new Error('Invalid option ID');
      }
    } catch (error) {
      console.error('Error casting vote:', error.message);
    }
  }
</script>

<main>
  <!-- Display options and votes -->
  {#each options as option}
    <div class="option" key={option.id}>
      <h3>{option.text}</h3>
      <p>Votes: {option.votes}</p>
      <button on:click={() => castVote(option.id)}>Vote</button>
    </div>
  {/each}
</main>

<style>
  .option {
    margin-bottom: 20px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
  }
  button {
    background-color: #007bff;
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 5px;
    cursor: pointer;
  }
  button:hover {
    background-color: #0056b3;
  }
</style>
