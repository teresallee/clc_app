<!-- This is the Javascript that adds functionality to the HTML -->
<script lang="ts">
	// This is where we hold all of the values that we change and manipulate.
	let now: number; //The current date in milliseconds. This value is set by setTimer and updateTimer.
	let countDownDate: Date; // The current date + the minutes (15, 30, 60) selected countDownDate. If a button is not clicked, this is undefined. This value is set by setTimer.

	let days = 0; // Default Value
	let hours = 0; // Default Value
	let minutes = 0; // Default Value
	let seconds = 0; // Default Value

	// This function will use the setInterval method to run the function that we have given it every second. This function will run every second whether we have a countDownDate or not but inside updateTimer, we check to see if a countDownDate is set. If it is not set we it will do nothing. If it is set, then go to updateTimer and read that.
	let thisRunsEverySecond = setInterval(updateTimer, 1000);

	// This function will take the date we give it, and add the number of minutes we give it. It will produce a new date such as 15 minutes into the future, and return it.
	function addMinutes(date: Date, minutes: number) {
		return new Date(date.getTime() + minutes * 60000);
	}

	// This function will set the timer time. It takes a parameter of minutes which is a number that represents minutes.
	function setTimer(minutes: number) {
		const date = new Date(); // Get the current date time so we can convert it to milliseconds so we can add the minutes (15, 30, 60) to it.
		now = date.getTime(); // Convert the current date time to milliseconds. We need it in milliseconds so we can do math with it. Otherwise we can't really do Feb 15 12pm - 30 minutes.
		countDownDate = addMinutes(date, minutes); // Set the timer countDownDate to this new date that we got from addMinutes(). Read into addMinutes().
	}

	// This function will update the timer every time it is run. Currently we run it every second on line 10.
	function updateTimer() {
		// If the countDownDate is not set by setTimer yet, then this function will do nothing. Otherwise it will compare subtract the currentDate in millisceonds from the countDownDate in milliseconds to show the remaining time.
		if (countDownDate) {
			// If countDownDate is set and is not undefined, then we wil update the days, hours, minutes, and seconds values.
			const date = new Date(); // Get the current time (when this function is running).
			now = date.getTime(); // Convert the current time into milliseconds. We need it in milliseconds so we can do math with it. Otherwise we can't really do Feb 15 12pm - 30 minutes.
			const timeleft = countDownDate.getTime() - now; // We convert countDownDate to milliseconds and minus the current date in milliseconds. This will calculate the difference between the countDownDate and current time giving us the time remaining.

			// Now we update the days, hours, minutes, seconds values.
			days = Math.floor(timeleft / (1000 * 60 * 60 * 24));
			hours = Math.floor((timeleft % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
			minutes = Math.floor((timeleft % (1000 * 60 * 60)) / (1000 * 60));
			seconds = Math.floor((timeleft % (1000 * 60)) / 1000);
		}
	}
</script>

<div class="center">
	<div class="grid grid-flow-col gap-5 text-center auto-cols-max">
		<!-- <div class="flex flex-col p-2 bg-neutral rounded-box text-neutral-content">
			<span class="countdown font-mono text-5xl">{days}</span>
			days
		</div> -->
		<div class="flex flex-col p-2 bg-neutral rounded-box text-neutral-content">
			<span class="countdown font-mono text-5xl">{hours}</span>
			hours
		</div>
		<div class="flex flex-col p-2 bg-neutral rounded-box text-neutral-content">
			<span class="countdown font-mono text-5xl">{minutes}</span>
			min
		</div>
		<div class="flex flex-col p-2 bg-neutral rounded-box text-neutral-content">
			<span class="countdown font-mono text-5xl">{seconds}</span>
			sec
		</div>
	</div>
</div>
<div class="button-container">
	<button
		class="btn mx-1"
		on:click={() => {
			setTimer(15);
		}}
	>
		15
	</button>
	<button
		class="btn mx-1"
		on:click={() => {
			setTimer(30);
		}}
	>
		30
	</button>
	<button
		class="btn mx-1"
		on:click={() => {
			setTimer(60);
		}}
	>
		60
	</button>
</div>

<!-- This is HTML in this HTML we use Tailwind and DaisyUI to set the styling and elements. -->
<style>
	.center {
		display: flex;
		justify-content: center;
		align-items: center;
		height: 20vh;
	}

	.button-container {
		display: flex;
		justify-content: center;
	}
</style>
