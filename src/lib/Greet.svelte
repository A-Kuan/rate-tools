<script lang="ts">

  const RATES = [
    3,8,10,15,30,100
  ]

  let price = 0;
  let rate = 3;

  let result = ""

  // 计算结果
  async function greet(){
    let _result = Number.parseFloat(""+(price+calPercnt(price,rate))).toFixed(2);
    if(_result === "NaN") {
      result = ""
    } else {
      result = _result;
    }
  }

  // 计算目标数的百分比结果
  function calPercnt(num: number, percentage: number){
    return num * (percentage / 100);
  }

  // 目标数值变化
  function change(event: any){
    price = Number.parseFloat(event.target.value);
    greet()
  }
</script>

<div>
  <form class="row" on:submit|preventDefault={greet}>
    <input on:input={change} type="number" step="0.01" id="greet-input" bind:value={price} placeholder="请输入进货价" />
    <!-- 比率 -->
    <select class="select-rates" name="rates" bind:value={rate}>
      {#each RATES as rate}
        <option value="{rate}">{`${rate}%`}</option>
      {/each}
    </select>
  </form>
  <br>
  <h1>{result}</h1>
</div>

<style>
  .select-rates {
    margin-right: 5px;
    appearance: none;
    text-align: center;
  }
</style>