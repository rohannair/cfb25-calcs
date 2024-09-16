<script lang="ts">
  const gradeOptions = [
    "A+", "A", "A-",
    "B+", "B", "B-",
    "C+", "C", "C-",
    "D+", "D", "D-",
    "F"
  ];

  const calculationMap: Record<string, number> = {
    "A+": 13, "A": 12, "A-": 11,
    "B+": 10, "B": 9, "B-": 8,
    "C+": 7, "C": 6, "C-": 5,
    "D+": 4, "D": 3, "D-": 2,
    "F": 1
  };

  function getResultColor(score: number): string {
    if (score > 30) return 'text-green-400';
    if (score > 20) return 'text-green-600';
    if (score >= 17 && score <= 20) return 'text-gray-400'; // Grey
    return 'text-red-500';
  }

  // biome-ignore lint/style/useConst: <explanation>
  let input1 = 'A+';
  // biome-ignore lint/style/useConst: <explanation>
  let input2 = "A+";
  // biome-ignore lint/style/useConst: <explanation>
  let input3 = "A+";

  $: result = calculationMap[input1] + calculationMap[input2] + calculationMap[input3];
</script>

<div class="bg-blue-400 absolute inset-0 flex justify-center items-center flex-col -mt-16 font-sans antialiased">
  <div class="flex flex-row space-x-4">
    <label class="flex flex-col gap-2">
      Stat 1
      <select
        name="input1"
        id="input1"
        bind:value={input1}
        class="p-2 border rounded"
      >
        {#each gradeOptions as grade}
          <option value={grade}>{grade}</option>
        {/each}
      </select>
    </label>
    <label class="flex flex-col gap-2">
      Stat 2
      <select
        name="input2"
        id="input2"
        bind:value={input2}
        class="p-2 border rounded"
      >
        {#each gradeOptions as grade}
          <option value={grade}>{grade}</option>
        {/each}
      </select>
    </label>
    <label class="flex flex-col gap-2">
      Stat 3
      <select
        name="input3"
        id="input3"
        bind:value={input3}
        class="p-2 border rounded"
      >
        {#each gradeOptions as grade}
          <option value={grade}>{grade}</option>
        {/each}
      </select>
    </label>
  </div>

  <p class={`mt-4 font-bold bg-gray-700 rounded-md p-2 ${getResultColor(result)}`}>
    Sum: {result} {result > 20 ? '😍' :  result >= 18 && result <= 20 ? '😐' : '😡'}
  </p>
</div>