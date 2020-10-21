<template>
    <div class="container">
        <h1>Tic Tac Toe</h1>
        <div>
            <h2 v-if="turn == 'X'">It's turn player: <span :class="turn">One</span></h2>
            <h2 v-else>It's turn player: <span :class="turn">Two</span></h2>
            <div class="gameFinished" v-if="findWinner">Congratulation, The winner is player {{winner[0] == 'X'? 'One':'Two'}}</div>
            <div class="draw" v-if="draw & turn">There is no winner</div>
            <table>
                <tr v-for="(row, i) in matrix" :key="i" @click="play">
                    <td v-for="(cell, ind) in row" :key="ind" :id="[i,ind]">{{cell}}</td>
                </tr>
            </table>
            <button @click="reset">Reset</button>
        </div>
    </div>
</template>

<script>
export default {
    name: "GameComponent",
    data(){
        return {
            game : [['','',''],['','',''],['','','']],
            c : 1,
            winner : '',
        };
    },
    computed : {
        matrix(){
            return this.game;
        },
        turn(){
            if(this.c % 2 == 0){
                return 'O';
            } else {
                return 'X';
            } 
        },
        findWinner(){
            if(this.winner == 'XXX' || this.winner == 'OOO'){
                return true;
            } else {
                return false;
            }
        },
        draw(){
            if (this.c === 10) {
                return true;
            }else {
                return false;
            }
        },
        done(){
            return "asd";
        }
    },
    methods : {
        play($evt){
            if (this.game[$evt.target.id[0]][$evt.target.id[2]] === '' && !this.findWinner) {
                var temp = this.game.slice(0);
                temp[$evt.target.id[0]][$evt.target.id[2]] = this.turn;
                this.c++;
                this.game = temp;
                this.win();
            }
        }, 
        win(){
            for(var i=0; i < this.game.length; i++){
                this.winner = this.game[i].join("");
                if(this.findWinner){
                    return;
                }
                var t = [];
                t.push(this.game[0][i])
                t.push(this.game[1][i])
                t.push(this.game[2][i])
                this.winner = t.join("");
                if(this.findWinner){
                    return;
                }
            }
            var tem1 = [];
            var tem2 = [];
            for(var j=0; j < this.game.length; j++){
                tem1.push(this.game[j][j])
                this.winner = tem1.join("");
                if(this.findWinner){
                    return;
                }
                tem2.push(this.game[j][this.game.length-1-j])
                this.winner = tem2.join("");
                if(this.findWinner){
                    return;
                }
            }
        },
        reset(){
            this.game = [['','',''],['','',''],['','','']];
            this.c = 1; 
            this.winner = ''
        }
    }
}
</script>

<style>
.container {
    text-align: center;
}

.gameFinished , .draw{
    font-family: arial, sans-serif;
    font-size: 50px;
    color: green;
}

.draw {
    color: red;
}

table {
    margin-top: 20px;
	margin-left: 430px;
	font-family: arial, sans-serif;
	border-collapse: collapse;
	border: 1px solid black;
}

td {
	border: 1px solid #dddddd;
	font-size: 30px;
	width: 50px;
	height: 50px;
}

table , td {
	border: 1px solid black;
	padding: 50px;
	text-align: center;
}

button {
    background-color: #000000;
    border: none;
    color: #FFFFFF;
    padding: 15px 32px;
    text-align: center;
    -webkit-transition-duration: 0.4s;
    transition-duration: 0.4s;
    margin: 16px 0 !important;
    text-decoration: none;
    font-size: 16px;
    cursor: pointer;
}

.X {
    color: red;
}
.O {
    color: blue;
}

</style>