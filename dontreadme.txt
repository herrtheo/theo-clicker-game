<!DOCTYPE html>
<head>
    <meta content="width=device-width, initial scale=1.0">
    <title>theo's clickgame</title>

    <style>
        #gameContainer {
            height: fit-content;
            width: 500px;

            color: green;
            line-height: 7px;

        }
        body {
            background-color: #35363A;
        }
        #click {
            height: 50px;
            width: fit-content;
            color: black;
            background-color: white;
            border-style: dashed;
        }
        #click:hover {
            background-color: grey;
            cursor: pointer;
            border-style: dotted;
        }
        .divBaseline {
            border-width: 2px;
            border-style: groove;
            border-color: green;

            display: inline-table;
            background-color: black;
            color: white;
            padding: 10px;
        }
        #shopContainer {
            width: 300px;
            height: 450px;
            margin-left: 5px;
        }
        #groupDivs {
            text-align: center;
            margin: auto;
        }
        .storeItem {
            background-color: darkslategray;
            height: 50px;
            display: inline-table;
            
            margin: 2px;
            font-size:small;
            
            border-style: solid;
            border-width: 1px;
            border-color: grey;
        }
        .buyButton {
            width: 50px;
            background-color: white;
            width: auto;
        }
        .buyButton:hover {
            cursor: pointer;
            background-color: grey;
        }
        #itemTab {
            color: white;
            font-size: small;
            background-color: black;

            border-width: 2px;
            border-color: green;
            border-style: groove;

            width: 150px;
            height: fit-content;
        }
        .MK_image {
            max-block-size: 28px;
        }
        #child_worker {
            max-block-size: 28px;
        }
        #cw_Alertbox {
            color: white;
        }
        #clickAmount {
            color: white;
        }
        #upgradesTab {
            width: 300px;
            height: fit-content;

            background-color: black;
            color: white;

        }
        .upgradeItem {
            background-color: darkslateblue;
            height: 50px;
            display: inline-table;
            
            margin: 2px;
            font-size:small;
            
            border-style: solid;
            border-width: 1px;
            border-color: grey;
        }
        .containerName {
            font-size: large;
            font-family:'Courier New', Courier, monospace;
            
            background-color: darkgreen;
        }
        #infoText {
            color: darkgreen;
        }
    </style>

</head>

<body>

    <div id="groupDivs">
        <div id="gameContainer" class="divBaseline">

            <p style="font-size:larger">Clicks = <span id="clickAmount">0</span></p>
            <button id="click" onclick="addClick()">+<span id="displayCPC">1</span></button>

            <p>clicks per second(cps): <span id="displayCPS">0</span></p>

            <div id="itemTab" class="divBaseline">
                <p class="containerName">Items;</p>
        
                <div style="display:table">
                    <p><img src="clicker game.info/pointer.png">Autoclicker: <span id="ac_Amount">0</span></p>
        
                    <p><img class="MK_image" src="clicker game.info/mk_item.png">MK: <span id="mk_Amount">0</span></p>
    
                    <p><img id="child_worker" src="clicker game.info/child_worker.png">Child workers: <span id="cw_Amount">0</span></p>
                </div> 
            </div>

        </div>

        <div id="shopContainer" class="divBaseline">

            <center><p class="containerName">Item store;</p></center>

            <div id="autoclickerItem" class="storeItem">
                <button class="buyButton" onclick="buyAutoclicker()">-<span id="ac_Cost">100</span></button>
                <p>Autoclicker, +1 CPS</p>
            </div>

            <div id="mkStoreItem" class="storeItem">
                <button class="buyButton" onclick="buyMK()">-<span id="mk_Cost">1000</span></button>
                <p>MK, +10 CPS & +<span id="MK_CPC">2</span>CPC</p>
            </div>

            <div id="childStoreItem" class="storeItem">
                <button class="buyButton" onclick="buyChildLabour()">-<span id="cw_Cost">100</span></button>
                <p>Every child worker gives 5cps, but dies after 30sec</p>
            </div>

        </div>

        <div id="upgradesTab" class="divBaseline">
            <p class="containerName">Upgrades;</p>

            <div class="upgradeItem">
                <button class="buyButton" onclick="upgradeClicks()">-<span id="doubleClick_Cost">500</span></button>

                <p>2x clicks for 10 min</p>
                <p>15 min cooldown</p>
            </div>

            <div class="upgradeItem">
                <button class="buyButton" onclick="upgradeMK()">-<span id="mkUpgrade_Cost">5000</span></button>

                <p>-25% of mk cost & x1.5  mk CPC.</p>
                <p>30 min cooldown</p>
            </div>

            <div class="upgradeItem">
                <button class="buyButton">-<span id="helt akho"></span>2500</button>

                <p>You become helt akho startklar, for 5 minutes:</p>
                <p>50% increase cps. 15 min cooldown</p>
            </div>

        </div>

    </div>

    <span id="alertbox"></span>

    <script>
        //variables
    
            var clickAmount = 10000;
            var cps = 0;
            var cpc = 1;
    
        //store items
    
            var ac_Cost = 100;
            var ac_Amount = 0;
    
            
            var mk_Cost = 1000;
            var mk_Amount = 0;
    
    
            var cw_Cost = 100;
            var cw_Amount = 0;

        //upgrades

            var dubClick_Cost = 500;
            let dubClick_Cooldown = 0;

            var upgradeMK_Cost = 5000;
            let upgradeMK_Cooldown = 0;

            var MK_CPC = 2;
    
        //gameFunctions
    
            function addClick() {
                clickAmount = clickAmount + cpc;
                document.getElementById("clickAmount").innerText = clickAmount;
            }
    
            setInterval(function(){
                clickAmount += cps;
                document.getElementById("clickAmount").innerHTML=Math.trunc(clickAmount);
                
                document.getElementById("alertbox").innerText = ""
    
            },1000)
    
        //Purchase items
    
            function buyAutoclicker() {
                if (clickAmount >= ac_Cost) {
                clickAmount -= ac_Cost;
                ac_Amount += 1;
                cps += 1;
    
                ac_Cost = ac_Cost * 1.01;
    
                document.getElementById("ac_Amount").innerText = ac_Amount;
                document.getElementById("ac_Cost").innerHTML=Math.trunc(ac_Cost);
                document.getElementById("displayCPS").innerText = cps;
                } else {alert("not enough clicks")}
            }
    
            function buyMK() {
                if (clickAmount >= mk_Cost) {
                clickAmount -= mk_Cost;
                mk_Amount += 1;
    
                cps += 10;
                cpc += 2;
    
                mk_Cost = mk_Cost * 1.1;
    
                document.getElementById("mk_Amount").innerText = mk_Amount;
                document.getElementById("mk_Cost").innerHTML=Math.trunc(mk_Cost);
    
                document.getElementById("displayCPS").innerText = cps;
                document.getElementById("displayCPC").innerText = cpc;
                } else {alert("not enough clicks")}
            }
    
            
    
            function buyChildLabour() {
                if (clickAmount >= cw_Cost) {
                clickAmount -= cw_Cost;
    
                cw_Amount += 1;
                cps += 5;
    
                document.getElementById("cw_Amount").innerText = cw_Amount;
                document.getElementById("displayCPS").innerText = cps;
    
                setTimeout(function(){
                    cw_Amount -= 1;
                    cps -= 5;
                    
                    document.getElementById("cw_Amount").innerText = cw_Amount;
                    document.getElementById("displayCPS").innerText = cps;
                    document.getElementById("cw_Alertbox").innerHTML = "one of your child workers has died.";
                },30000)
                setTimeout(function(){
    
                    document.getElementById("alertbox").innerHTML = "";
    
                },30500)
                } else {alert("not enough clicks")}
            }

            function upgradeClicks() {
                if (dubClick_Cooldown <= 0 && clickAmount >= dubClick_Cost) {
                        clickAmount -= dubClick_Cost;
                        dubClick_Cooldown += 1;
                        cpc *= 2;

                        document.getElementById("doubleClick_Cost").innerText = "on cooldown";
                        document.getElementById("displayCPC").innerText = cpc;

                    setTimeout(function(){
                            dubClick_Cost *= 1.25;
                            dubClick_Cooldown -= 1;
                            cpc *= 0.5;

                            document.getElementById("doubleClick_Cost").innerHTML=Math.trunc(dubClick_Cost);
                            document.getElementById("displayCPC").innerText=Math.trunc(cpc);
                            
                            document.getElementById("alertbox").innerText = "Double click is now off cooldown."
                        
                    },600000)

                    setTimeout(function(){
                        document.getElementById("alertbox").innerText = ""
                    },601500)
                } else {alert("not enough clicks, or on cooldown")}
            }

            let x_mk = 1.5;

            function upgradeMK() {
                if (upgradeMK_Cooldown <= 0 && clickAmount >= upgradeMK_Cost) {

                clickAmount -= upgradeMK_Cost;
                upgradeMK_Cooldown += 1;
                mk_Cost *= 0.75;
                MK_CPC *= 1.5;

                x_mk *= mk_Amount;
                cpc += x_mk;

                document.getElementById("MK_CPC").innerText = MK_CPC;
                document.getElementById("mk_Cost").innerHTML=Math.trunc(mk_Cost);
                document.getElementById("displayCPC").innerText = cpc;
                document.getElementById("mkUpgrade_Cost").innerText = "on cooldown";
                document.getElementById("alertbox").innerText = "";


                setTimeout(function() {
                    upgradeMK_Cost *= 1.5;
                    upgradeMK_Cooldown -= 1;

                    document.getElementById("mkUpgrade_Cost").innerText = upgradeMK_Cost;
                    document.getElementById("alertbox").innerText = "mk upgrade is now off cooldown";
                },1800)

                } else {alert("not enough clicks, or on cooldown.")}
            }
    
        </script>

    <p id="infoText">"if you reload page, your progress will be lost."</p>

</body>
