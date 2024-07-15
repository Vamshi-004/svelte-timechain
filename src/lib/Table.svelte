<script>
  export let names;

  let showUpdateForm = false;
  let currentUserId = 0;

  function openUpdateForm(userId) {
    currentUserId = userId;
    showUpdateForm = true;
  }

  function closeUpdateForm() {
    showUpdateForm = false;
  }
</script>

<div
  class="mt-10 pt-10 w-full max-w-xl p-12 mx-auto rounded-lg shadow-xl dark:bg-white/10 bg-white/30 ring-1 ring-gray-900/5 backdrop-blur-lg"
>
  <div class="flex items-center justify-between mb-4">
    <div class="space-y-1">
      <h2 class="text-xl font-semibold">List of Users</h2>
      <p class="text-sm text-gray-500">
        Fetched {names.length} users
      </p>
    </div>
  </div>
  <div class="divide-y divide-gray-900/5">
    {#each names as user (user.id)}
      <div class="flex items-center justify-between py-3">
        <div class="flex flex-col items-start space-y-1">
          <p class="font-medium leading-none break-all">{user.name}</p>
          <p class="font-medium text-gray-500 break-all">{user.email}</p>
        </div>
        <div class="flex items-center space-x-4">
          <button
            type="submit"
            class="text-white font-bold px-2 rounded float-right"
            on:click={() => openUpdateForm(user.id)}
          >
            <img class="w-4" src="./pencil.svg" alt="update" />
          </button>
          <form method="POST" action="/profiles?/delete">
            <input type="hidden" name="id" id="id" value={user.id} />
            <button type="submit">
              <img class="w-4" src="./trash-can.svg" alt="delete" />
            </button>
          </form>
        </div>
      </div>
    {/each}
  </div>
</div>

<!-- Update Modal -->
{#if showUpdateForm}
  <div
    class="fixed inset-0 flex items-center justify-center z-50 bg-black bg-opacity-50"
  >
    <div class="bg-white p-6 rounded-lg shadow-md w-96">
      <h2 class="text-xl font-semibold mb-4">Update User</h2>
      <form method="POST" action="/profiles?/update">
        <input type="hidden" name="id" id="id" value={currentUserId} />
        <div class="flex flex-wrap -mx-3 mb-2">
          <div class="w-full md:w-1/2 px-3 mb-6 md:mb-0">
            <label
              class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
              for="grid-name"
            >
              Name
            </label>
            <input
              class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
              id="name"
              type="text"
              placeholder="Enter name"
              name="name"
            />
          </div>
          <div class="w-full md:w-1/2 px-3 mb-6 md:mb-0">
            <label
              class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
              for="grid-email"
            >
              Email
            </label>
            <input
              class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
              id="email"
              type="text"
              placeholder="Enter email"
              name="email"
            />
          </div>
        </div>
        <div class="flex justify-end space-x-2 mt-4">
          <button
            type="submit"
            class="bg-yellow-500 hover:bg-blue-700 text-white font-bold px-4 py-2 rounded"
          >
            Update User
          </button>
          <button
            type="button"
            class="bg-gray-500 hover:bg-gray-700 text-white font-bold px-4 py-2 rounded"
            on:click={closeUpdateForm}
          >
            Cancel
          </button>
        </div>
      </form>
    </div>
  </div>
{/if}
