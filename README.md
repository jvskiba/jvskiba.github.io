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
				<div id="Top" style="height: 60%">
					<p>Buy</p>
					<div>
						<button onclick="ButtonMultiplyer(1)" type="button">Buy X1</button>
						<button onclick="ButtonMultiplyer(10)" type="button">Buy X10</button>
						<button onclick="ButtonMultiplyer(100)" type="button">Buy X100</button>
						<p id="MultiplyerPar"></p>
					</div>
					<button onclick="ButtonPressed(0)" onmouseover="SetInfo(1,0)" onmouseout="SetInfo(0,0)" type="button">Click for money</button><br>
					<button onclick="ButtonPressed(3)" onmouseover="SetInfo(1,3)" onmouseout="SetInfo(0,3)" type="button">Motivate Teachers</button><br>
					<button onclick="ButtonPressed(1)" onmouseover="SetInfo(1,1)" onmouseout="SetInfo(0,1)" type="button">Buy a Teacher</button><br>
					<button onclick="ButtonPressed(2)" onmouseover="SetInfo(1,2)" onmouseout="SetInfo(0,2)" type="button">Buy a Students</button><br>
					<button onclick="ButtonPressed(4)" onmouseover="SetInfo(1,4)" onmouseout="SetInfo(0,4)" type="button">Buy a teacher a PHD</button><br>
					<button onclick="ButtonPressed(5)" onmouseover="SetInfo(1,5)" onmouseout="SetInfo(0,5)" type="button">Buy a Professer</button><br>
					<button onclick="ButtonPressed(6)" onmouseover="SetInfo(1,6)" onmouseout="SetInfo(0,6)" type="button">Buy a Custodian</button><br>
					<button onclick="ButtonPressed(7)" onmouseover="SetInfo(1,7)" onmouseout="SetInfo(0,7)" type="button">Buy a Physicist</button><br>
					<button onclick="ButtonPressed(8)" onmouseover="SetInfo(1,8)" onmouseout="SetInfo(0,8)" type="button">Buy a Engineer</button>
					<button onclick="robotEngineer()" type="button">Buy a Robo student</button><br>
				</div>
				<div id="Bottom" style="height: 40%">
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
			<p>Student engineer</p>
			<p id="7"></p>
			<p id="7.5"></p>
		</div>
		<body style="text-align:center;" onload="start()">
		</body>
	</div>
	<script>
		//         cost to produce^   ^How much they produce
		//               [0, 50, .5, .5]
		//	  amount owned^   ^price to buy                                                                                                  Length till next stu^
		var GameStat = [[0, 0],[0, 0],[0, 25 , 0, 1],[0, 50, .5, .5],[0, 70, 3], [0, 1000, 10, 50],
		[0, 10, 0, 100, 500],[0, 1000, 25, 200], [0, 10, 1000, 1, 60, true], [0, 1000, 150, 250]];
		var numsWithCommas = [0,0,0,0,0,0,0,0,0,0]
		var ButtonInfoArray = [
		"Click to earn $0.5 instantly.",	
		"Click to buy a teacher for $25. Each teacher produces 1 math every second.",
		"Click to buy a student for 50 math. They produce $0.5 every second for a cost of .5 math.",
		"Click to add .25 math per teacher owned.",
		"Click to give a teacher a PHD for $70 and it increases their math prduction by 3 times. You can give one phd per teacher.", 
		"Click to buy a professor, they cost 1000. But they cost $10 per second and produce 50 math a second.You need a teacher to do this",
		"Click to buy a custodian, they cost $1,000 and find $100 1 out of 100 times.",
		"Click to buy a physisist which produces 200 math for a cost of $25. You need a professor to do this.",
		"IDK"]
		var InfoToDisplay = "";
		var ErrorToDisplay = "";
		var FrameRate = 10;
		var USInt;
		var UInt;
		var TimeInt;
		var TimerVal = 0;
		var TimeOpen = 0;
		var BuyMultiplyer = 1;

		
		function start() {
			var Time = 1000/FrameRate;
			UInt = setInterval(Update, 1000);
			USInt = setInterval(UpdateScreen, Time);
			TimeInt = setInterval(TimeOpen, 100);
			TimerDisplay(4, "Wellcome, I suggest you hover over the buttons to know what they do.");
		}
		 
		function TimeOpenFunc() {
			TimeOpen = TimeOpen + 0.1;
		}
		
		function Update() {
			PreCheck(GameStat[2][2], 0, GameStat[2][3], 0, GameStat[2][0], 1, GameStat[4][2], GameStat[4][0]);
			PreCheck(GameStat[3][2], 0, GameStat[3][3], 1, GameStat[3][0], 0, 1, 0);
			PreCheck(GameStat[5][2], 1, GameStat[5][3], 0, GameStat[5][0], 0, 1, 0);
			PreCheck(GameStat[7][2], 1, GameStat[7][3], 0, GameStat[7][0], 0, 1, 0);
			PreCheck(GameStat[9][2], 0, GameStat[9][3], 1, GameStat[9][0], 0, 1, 0);
			custodian();
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
			for (var i = 0; i < GameStat.length; i++) {
				numsWithCommas[i] = addCommas(GameStat[i][0])
			}
			document.getElementById("0").innerHTML = numsWithCommas[0];
			document.getElementById("1").innerHTML = numsWithCommas[1];
			document.getElementById("2").innerHTML = numsWithCommas[2];
			document.getElementById("2.5").innerHTML = numsWithCommas[4];
			document.getElementById("3").innerHTML = numsWithCommas[3];
			document.getElementById("4").innerHTML = numsWithCommas[5];
			document.getElementById("5").innerHTML = numsWithCommas[6];
			document.getElementById("6").innerHTML = numsWithCommas[7];
			document.getElementById("7").innerHTML = numsWithCommas[8];
			document.getElementById("7.5").innerHTML = numsWithCommas[9];
			document.getElementById("InfoBox").innerHTML = InfoToDisplay;
			document.getElementById("ErrorBox").innerHTML = ErrorToDisplay;
			document.getElementById("MultiplyerPar").innerHTML = BuyMultiplyer;
		}
		
		function PreCheck(Price, fromWhat, addNum, toWhat, neededItem, UseCount, multiplyer, NeededItem2) {
			if (neededItem > 0) {
				for (var i = 0; i < neededItem; i++) {
					if (UseCount == 0) {
						CheckAndAdd(Price, fromWhat, addNum, toWhat, 1, 1)
					} else {
						if (GameStat[fromWhat][0] >= Price) {	
							if (i < NeededItem2) {CheckAndAdd(Price, fromWhat, addNum, toWhat, multiplyer, 1)}
							else {CheckAndAdd(Price, fromWhat, addNum, toWhat, 1, 1)}
						}
					}	
				}
			}
		}
		
		function SinglePreCheck(Price, fromWhat, addNum, toWhat, neededItem, UseBuyMulti) {
			if (neededItem > 0) {
				if (UseBuyMulti == true) {CheckAndAdd(Price, fromWhat, addNum, toWhat, 1, BuyMultiplyer)}
				else {CheckAndAdd(Price, fromWhat, addNum, toWhat, 1, 1)}
			} else {TimerDisplay(2, "You don't have the needed item to get this.")}
		}
		
		function CheckAndAdd(Price, fromWhat, addNum, toWhat, AddMulti, BuyMulti) {
			if (GameStat[fromWhat][0] >= (Price * BuyMulti)) {
				GameStat[fromWhat][0] -= (Price * BuyMulti);
				GameStat[toWhat][0] += (addNum * AddMulti * BuyMulti);
			} else {
				TimerDisplay(2, "You don't have enuough money to buy this")
			}
		}
		
		function getRndInteger(min, max) {
			return Math.floor(Math.random() * (max - min) ) + min;
		}
		
		function ButtonPressed(Func) {
			if (Func == 0) {GameStat[1][0] = GameStat[1][0] + 0.5;}
			if (Func == 1) {SinglePreCheck(GameStat[2][1], 1, 1, 2, 1, true)}
			if (Func == 2) {SinglePreCheck(GameStat[3][1], 0, 1, 3, 1, true)}
			if (Func == 3) {PreCheck(0, 0, .25, 0, GameStat[2][0], 0, 0, 0)}
			if (Func == 4) {if (GameStat[2][0] > (GameStat[4][0] * BuyMultiplyer)) {SinglePreCheck(GameStat[4][1], 1, 1, 4, GameStat[2][0], true)}}
			if (Func == 5) {SinglePreCheck(GameStat[5][1], 1, 1, 5, GameStat[1][0], true)}
			if (Func == 6) {SinglePreCheck(GameStat[6][1], 1, 1, 6, GameStat[1][0], true)}
			if (Func == 7) {SinglePreCheck(GameStat[7][1], 1, 1, 7, GameStat[5][0], true)}
			if (Func == 8) {SinglePreCheck(GameStat[8][1], 1, 1, 8, 1, true)}
		}
		
		function SetInfo(OnOff, Func) {
			if (OnOff == 1) {InfoToDisplay = ButtonInfoArray[Func];}
			if (OnOff == 0) {InfoToDisplay = "";}
		}
		
		function TimerDisplay(Length, Message) {
			ErrorToDisplay = Message;
			Length *= 1000;
			setTimeout(function(){ErrorToDisplay = "";}, Length);
		}
		
		function ButtonMultiplyer(Multiplyer) {
			BuyMultiplyer = Multiplyer;
		}
		
		function robotEngineer() {
			if (GameStat[1][0] >= GameStat[9][1]) {
				GameStat[1][0] -= GameStat[9][1]
				console.log("Engineer")
				waitTime = GameStat[8][4] / GameStat[8][0] * 1000;
				if (GameStat[8][5] == true) {
					GameStat[8][5] = true
					GameStat[9][0] += 1; 
					setTimeout(function(){GameStat[8][5] = true;}, waitTime);
				}
			}
		}
		function addCommas(nStr) {
			nStr += '';
			var x = nStr.split('.');
			var x1 = x[0];
			var x2 = x.length > 1 ? '.' + x[1] : '';
			var rgx = /(\d+)(\d{3})/;
			while (rgx.test(x1)) {
				x1 = x1.replace(rgx, '$1' + ',' + '$2');
			}
			return x1 + x2;
		}
		
	</script>
</html>
