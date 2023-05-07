<script lang="ts">
   let countDownDate: Date // Place holder for the countDownDate.
	let now: number //The current date in milliseconds.
	let days = 0 // Default Value
	let hours = 0 // Default Value
	let minutes = 0 // Default Value
	let seconds = 0 // Default Value

   // This function will use the setIntervalMethod to run the function that we have given it.
	let thisRunsEverySecond = setInterval(updateTimer, 1000);

   // This function will take the date we give it, and add the number of minutes we give it. It will produce a new date such as 15 minutes into the future, and return it. 
	function addMinutes(date: Date, minutes: number) {
		return new Date(date.getTime() + minutes * 60000);
	}

   // This function will set the timer time.
	function setTimer(buttonTime: number) {
		const date = new Date(); // Get the current date time.
		now = date.getTime(); // Convert the current date time to milliseconds.
      countDownDate = addMinutes(date, buttonTime) // Set the timer countDownDate to this new date that we got from addMinutes().
	}

   // This function will update the timer every time it is run. Currently we run it every second on line 10.
	function updateTimer () {
      if (countDownDate) { // If countDownDate is set and is not undefined, then we wil update the days, hours, minutes, and seconds values.
         const date = new Date(); // Get the current time (when this function is running).
         now = date.getTime(); // Convert the current time into milliseconds.
         const timeleft = countDownDate - now; // Calculate the difference between the countDownDate and current time. 

         // Now we update the days, hours, minutes, seconds values.
         days = Math.floor(timeleft / (1000 * 60 * 60 * 24));
         hours = Math.floor((timeleft % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
         minutes = Math.floor((timeleft % (1000 * 60 * 60)) / (1000 * 60));
         seconds = Math.floor((timeleft % (1000 * 60)) / 1000);
      }
	}
</script>

<h1>this is homepage</h1>

<!-- 
[15 minutes] - figure out what the time is 15 minutes into the future. use this time in line 2
 [30 minutes] -->

<div class="grid grid-flow-col gap-5 text-center auto-cols-max">
	<!-- <div class="flex flex-col p-2 bg-neutral rounded-box text-neutral-content">
		<span class="countdown font-mono text-5xl">
			{days}
		</span>
		days
	</div> -->
	<div class="flex flex-col p-2 bg-neutral rounded-box text-neutral-content">
		<span class="countdown font-mono text-5xl">
			{hours}
		</span>
		hours
	</div>
	<div class="flex flex-col p-2 bg-neutral rounded-box text-neutral-content">
		<span class="countdown font-mono text-5xl">
			{minutes}
		</span>
		min
	</div>
	<div class="flex flex-col p-2 bg-neutral rounded-box text-neutral-content">
		<span class="countdown font-mono text-5xl">
			{seconds}
		</span>
		sec
	</div>
</div>
<button
	class="btn mt-5"
	on:click={() => {
		setTimer(15);
	}}>15</button
>
<button class="btn">30</button>
