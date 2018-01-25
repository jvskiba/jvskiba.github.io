<!DOCTYPE html>

<html>
	<head>
		<style>
			h1 {
				text-align: center;
			}

			p {
				text-align: center;
			}
			#container {
    
			}
			#Bottom {
				position: absolute;
				bottom: 0;
			}
			#Top {
				position: absolute;
				Top: 0;
			}
		</style>
	</head>
	<div id="container">
		<div style="width: 50%; float:left">	
			<div style="width: 50%; float: right;">
				<h1>Dr.Math</h1>
				<p id="InfoBox"></p>
				<p id="ErrorBox"></p>
			</div>
			<div style="width: 50%; float: left;">
				<div id="Top">
					<p>Buy</p>
					<button onclick="ButtonPressed(0)" onmouseover="SetInfo(1,0)" onmouseout="SetInfo(0,0)" type="button">Click for money</button><br>
					<button onclick="ButtonPressed(3)" onmouseover="SetInfo(1,3)" onmouseout="SetInfo(0,3)" type="button">Motivate Teachers</button><br>
					<button onclick="ButtonPressed(1)" onmouseover="SetInfo(1,1)" onmouseout="SetInfo(0,1)" type="button">Buy Teacher</button><br>
					<button onclick="ButtonPressed(2)" onmouseover="SetInfo(1,2)" onmouseout="SetInfo(0,2)" type="button">Buy Students</button><br>
					<button onclick="ButtonPressed(4)" onmouseover="SetInfo(1,4)" onmouseout="SetInfo(0,4)" type="button">Buy a teacher a PHD</button><br>
					<button onclick="ButtonPressed(5)" onmouseover="SetInfo(1,5)" onmouseout="SetInfo(0,5)" type="button">Buy a Professer</button><br>
					<button onclick="ButtonPressed(6)" onmouseover="SetInfo(1,6)" onmouseout="SetInfo(0,6)" type="button">Buy a Custodian</button><br>
					<button onclick="ButtonPressed(7)" onmouseover="SetInfo(1,7)" onmouseout="SetInfo(0,7)" type="button">Buy a Physisist</button><br>
				</div>
				<div id="Bottom">
					<p>Upgrades</p>
				</div>
			</div>
		</div>

		<div style="width: 50%; float:right">
			<p>Math</p>
			<p id="0"></p>
			<p>Money</p>
			<p id="1"></p>
			<p>Math teachers</p>
			<p id="2"></p>
			<p id="2.5"></p>
			<p>Students</p>
			<p id="3"></p>
			<p>Professers</p>
			<p id="4"></p>
			<p>Custodian</p>
			<p id="5"></p>
			<p>Physicists</p>
			<p id="6"></p>
		</div>
		<body style="text-align:center;" onload="start()">
		</body>
	</div>
	<script>
		//         cost to produce^   ^How much they produce
		//               [0, 50, .5, .5]
		//	  amount owned^   ^price to buy
		var GameStat = [[0, 0],[0, 0],[0, 25 , 0, 1],[0, 50, .5, .5],[0, 70, 3], [0, 1000, 10, 50], [0, 10, 0, 100, 100],[0, 1000, 25, 200]];
		var ButtonInfoArray = [
		"Click to earn $0.5 instantly.",	
		"Click to buy a teacher for $25. Each teacher produces 1 math every second.",
		"Click to buy a student for 50 math. They produce $0.5 every second for a cost of .5 math.",
		"Click to add .25 math per teacher owned.",
		"Click to give a teacher a PHD for $70 and it increases their math prduction by 3 times.", 
		"Click to buy a professor, they cost 1000. But they cost $10 per second and produce 50 math a second.",
		"Click to buy a custodian, they cost $1,000 and find $100 1 out of 100 times.",
		"Click to buy"]
		var InfoToDisplay = "";
		var ErrorToDisplay = "";
		var FrameRate = 10;
		var USInt;
		var UInt;
		var TimeInt;
		var TimerVal = 0;
		var TimeOpen = 0;
		
		function start() {
			var Time = 1000/FrameRate;
			UInt = setInterval(Update, 1000);
			USInt = setInterval(UpdateScreen, Time);
			TimeInt = setInterval(TimeOpen, 100);
			TimerDisplay(4, "Wellcome, I sudgest you hover over the buttons to know what they do.")
		}
		 
		function TimeOpenFunc() {
			TimeOpen = TimeOpen + 0.1
		}
		
		function Update() {
			PreCheck(GameStat[2][2], 0, GameStat[2][3], 0, GameStat[2][0], 1, GameStat[4][2], GameStat[4][0])
			PreCheck(GameStat[3][2], 0, GameStat[3][3], 1, GameStat[3][0], 0, 1, 0)
			PreCheck(GameStat[5][2], 1, GameStat[5][3], 0, GameStat[5][0], 0, 1, 0)
			PreCheck(GameStat[7][2], 1, GameStat[7][3], 0, GameStat[7][0], 0, 1, 0)
			custodian()
		}
		
		function custodian(){
			for (var i = 0; i < GameStat[6][0]; i++) {
				var RndInterger = getRndInteger(0, GameStat[6][4]);
				console.log(RndInterger)
				if (RndInterger == 0) {
					GameStat[1][0] = GameStat[1][0] + GameStat[6][3];
				}
			}
			
		}
		
		function UpdateScreen() {
			document.getElementById("0").innerHTML = GameStat[0][0];
			document.getElementById("1").innerHTML = GameStat[1][0];
			document.getElementById("2").innerHTML = GameStat[2][0];
			document.getElementById("2.5").innerHTML = GameStat[4][0];
			document.getElementById("3").innerHTML = GameStat[3][0];
			document.getElementById("4").innerHTML = GameStat[5][0];
			document.getElementById("5").innerHTML = GameStat[6][0];
			document.getElementById("6").innerHTML = GameStat[7][0];
			document.getElementById("InfoBox").innerHTML = InfoToDisplay;
			document.getElementById("ErrorBox").innerHTML = ErrorToDisplay;
		}
		
		function PreCheck(Price, fromWhat, addNum, toWhat, neededItem, UseCount, multiplyer, NeededItem2) {
			if (neededItem > 0) {
				for (var i = 0; i < neededItem; i++) {
					if (UseCount == 0) {
						CheckAndAdd(Price, fromWhat, addNum, toWhat, 1)
					} else {
						if (GameStat[fromWhat][0] >= Price) {	
							if (i < NeededItem2) {CheckAndAdd(Price, fromWhat, addNum, toWhat, multiplyer)}
							else {CheckAndAdd(Price, fromWhat, addNum, toWhat, 1)}
						}
					}	
				}
			}
		}
		
		function CheckAndAdd(Price, fromWhat, addNum, toWhat, multiplyer) {
			if (GameStat[fromWhat][0] >= Price) {
				GameStat[fromWhat][0] = GameStat[fromWhat][0] - Price;
				GameStat[toWhat][0] = GameStat[toWhat][0] + (addNum * multiplyer);
			} else {
				TimerDisplay(1.5, "You don't have enuough money to buy this")
			}
		}
		
		function SinglePreCheck(Price, fromWhat, addNum, toWhat, neededItem) {
			if (neededItem > 0) {
				CheckAndAdd(Price, fromWhat, addNum, toWhat, 1)
			} else {TimerDisplay(1.5, "You don't have the needed item to get this.")}
		}
		
		function getRndInteger(min, max) {
			return Math.floor(Math.random() * (max - min) ) + min;
		}
		
		function ButtonPressed(Func) {
			if (Func == 0) {GameStat[1][0] = GameStat[1][0] + 0.5;}
			if (Func == 1) {CheckAndAdd(GameStat[2][1], 1, 1, 2, 1)}
			if (Func == 2) {SinglePreCheck(GameStat[3][1], 0, 1, 3, 1)}
			if (Func == 3) {PreCheck(0, 0, .25, 0, GameStat[2][0], 0, 0, 0)}
			if (Func == 4) {if (GameStat[2][0] > GameStat[4][0]) {SinglePreCheck(GameStat[4][1], 1, 1, 4, GameStat[2][0])}}
			if (Func == 5) {SinglePreCheck(GameStat[5][1], 1, 1, 5, GameStat[1][0])}
			if (Func == 6) {SinglePreCheck(GameStat[6][1], 1, 1, 6, GameStat[1][0])}
			if (Func == 7) {SinglePreCheck(GameStat[7][1], 1, 1, 7, GameStat[5][0])}
		}
		
		function SetInfo(OnOff, Func) {
			if (OnOff == 1) {InfoToDisplay = ButtonInfoArray[Func];}
			if (OnOff == 0) {InfoToDisplay = "";}
		}
		
		function TimerDisplay(Length, Message) {
			ErrorToDisplay = Message;
			Length = Length * 1000;
			setTimeout(function(){ErrorToDisplay = "";}, Length);
		}
		
		
	</script>
</html>
