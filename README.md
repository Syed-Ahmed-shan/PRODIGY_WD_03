# PRODIGY_WD_03
 This is the HTML code.....

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TicTacToe</title>
    <link rel="stylesheet" href="tic.css">
</head>
<body>
    <div class="turn-cointainer">
        <h3>Turn for</h3>
        <div class="turn-box align">X</div>
        <div class="turn-box align">O</div>
        <div class="bg"></div>
    </div>
    <div class="main-grid">
        <div class="box align" style="--clr:#1F51FF">0</div>
        <div class="box align" style="--clr:#1F51FF">1</div>
        <div class="box align" style="--clr:#1F51FF">2</div>
        <div class="box align" style="--clr:#1F51FF">3</div>
        <div class="box align" style="--clr:#1F51FF">4</div>
        <div class="box align" style="--clr:#1F51FF">5</div>
        <div class="box align" style="--clr:#1F51FF">6</div>
        <div class="box align" style="--clr:#1F51FF">7</div>
        <div class="box align" style="--clr:#1F51FF">8</div>
    </div>
    <h2 id="results">X Win</h2>
    <button id="play-again" style="--clr:#ab20fd">Play Again</button>
    <script src="tic.js">

    </script>
</body>
</html> 

This is the CSS code for the tic tac toe 

*{
    color: aliceblue;
    font-family: serif;
    transition: 0.2s easy-in-out;
    user-select: none;

}
.align{
    display: flex;
    justify-content: center;
    align-items: center;

}
body{
   
   
    background-color: #252A34;
    margin: 0;
    padding: 0;
    width: 100vw;
    text-align: center;
    padding-top: 6vh;
}
.turn-cointainer{
  
    width: 170px;
    height: 80px;
    margin: auto;
    display: grid;
    grid-template: 1fr;
    grid-template-rows: 1fr 1fr;
    position: relative;
    border-radius: 8px;
}
.turn-cointainer h3{
    margin: 0;
    grid-column-start: 1;
    grid-column-end: 3;
}
.turn-cointainer .turn-box{
    border: 3px solid #000;
    font-size: 1.6rem;
    font-weight: 700;
}
.turn-cointainer .turn-box:nth-child(even){
    border-right: none;
}
.bg{
    position: absolute;
    bottom: 0;
    left: 0;
    width: 85px;
    height: 40px;
    background-color: rgb(190, 142, 190);
    z-index: -1;
}
.main-grid{
    background-image:  url("https://img.freepik.com/free-photo/abstract-grunge-decorative-relief-navy-blue-stucco-wall-texture-wide-angle-rough-colored-background_1258-28311.jpg?auto=format&fit=crop&w=315&h=220");
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(3, 1fr);
    height: 250px;
    width: 250px;
    margin: 40px auto;
    border: 0 solid#fff;
    border-radius: 8px;
    box-shadow: 0 0 7px 7px  #fff;
}
.box {
    cursor: pointer;
    cursor: -moz-zoom-in;
    cursor: -moz-zoom-out;
    font-size: 3rem;
    font-weight: 700;
    border: 2px solid #fff;

}
.box:hover{
    background-color: #65afc890;
    color: black;
    box-shadow: 0 0 55px var(--clr);
}

#play-again{
    background-color: #000;
    padding: 10px 25px;
    border: 0 0 35px;
    font-size: 1.5rem;
    border-radius: 8px;
    cursor: pointer;
    border-color: rgb(174, 104, 206);
    
}

#play-again:hover{
    padding: 10px 10px;
    letter-spacing: 0.30em;
    background: var(--clr);
    box-shadow: 0 0 35px var(--clr);
    background-color: #b47ce5;
}
h3{
    text-decoration:red underline;
    text-shadow: 2px 4px 4px  #e3d2d2;
}


This is the Java Code For the TIC TAC TOE 

let boxes = document.querySelectorAll(".box");

let turn = "X";
let isGameOver = false;

boxes.forEach(e =>{
    e.innerHTML = ""
    e.addEventListener("click", ()=>{
        if(!isGameOver && e.innerHTML === ""){
            e.innerHTML = turn;
            cheakWin();
            cheakDraw();
            changeTurn();
        }
    })
})

function changeTurn(){
    if(turn === "X"){
        turn = "O";
        document.querySelector(".bg").style.left = "85px";
    }
    else{
        turn = "X";
        document.querySelector(".bg").style.left = "0";
    }
}

function cheakWin(){
    let winConditions = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8],
        [0, 3, 6], [1, 4, 7], [2, 5, 8],
        [0, 4, 8], [2, 4, 6]
    ]
    for(let i = 0; i<winConditions.length; i++){
        let v0 = boxes[winConditions[i][0]].innerHTML;
        let v1 = boxes[winConditions[i][1]].innerHTML;
        let v2 = boxes[winConditions[i][2]].innerHTML;

        if(v0 != "" && v0 === v1 && v0 === v2){
            isGameOver = true;
            document.querySelector("#results").innerHTML = turn + " win";
            document.querySelector("#play-again").style.display = "inline"

            for(j = 0; j<3; j++){
                boxes[winConditions[i][j]].style.backgroundColor = "#08D9D6"
                boxes[winConditions[i][j]].style.color = "#000"
            }
        }
    }
}

function cheakDraw(){
    if(!isGameOver){
        let isDraw = true;
        boxes.forEach(e =>{
            if(e.innerHTML === "") isDraw = false;
        })

        if(isDraw){
            isGameOver = true;
            document.querySelector("#results").innerHTML = "Draw";
            document.querySelector("#play-again").style.display = "inline"
        }
    }
}

document.querySelector("#play-again").addEventListener("click", ()=>{
    isGameOver = false;
    turn = "X";
    document.querySelector(".bg").style.left = "0";
    document.querySelector("#results").innerHTML = "";
    document.querySelector("#play-again").style.display = "none";

    boxes.forEach(e =>{
        e.innerHTML = "";
        e.style.removeProperty("background-color");
        e.style.color = "#fff"
    })
})




