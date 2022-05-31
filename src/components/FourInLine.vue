<template>
    <div>
        <div class="row text-center mt-3">
            <div class="col-12 d-flex justify-content-center">
                <div class="gameboard">
                    <div v-for="(n, i) in 4">
                        <div v-for="(n, j) in 4">
                            <Square @click="markSquare(i, j)" :value="gameboard[i][j]"></Square>
                        </div>
                    </div>
                </div>
            </div>
            <div class="col-12">
                <div class="player-turn">
                    Es el turno de: 
                    <span class="text-dark fw-bold text-uppercase">
                        "{{ activePlayerMarker }}"
                    </span>
                </div>
                <div class="winner" v-if="winner !== ''">
                    Ha ganado: "{{winner}}"
                </div>
                <button class="btn btn-dark rounded-pill fw-bold" @click="resetGame">Reiniciar</button>
            </div>
        </div>
    </div>
</template>

<style>
    body{
        background: #5596ff;
    }
    .gameboard{
        display: flex;
        flex-wrap: wrap;
        width: 270px;
        height: 270px;
        border: 7px solid #ffffff;
        border-radius: 5px;

    }
    .player-turn {
        font-size: 20px;
        font-weight: bold;
        color: white;
    }
    .winner {
        font-size: 40px;
        color: rgb(246, 255, 0);
    }
</style>

<script>
import Square from './Square.vue'
export default {
    data() {
        return {
            gameboard: [
                ['', '', '', ''],
                ['', '', '', ''],
                ['', '', '', ''],
                ['', '', '', '']
            ],
            activePlayerMarker: 'x',
            winner: '',
        };
    },

    methods: { 
        markSquare(i, j){
            if(this.gameboard[i][j] !== '' || this.winner !== ''){ return; }
            this.gameboard[i][j] = this.activePlayerMarker;
            this.$forceUpdate();
            this.verifyMove();
        },
        verifyMove(){
            var scoresArray = [];
            for(let i in this.gameboard){
                let stringScore = this.gameboard[i].reduce((a, b) => a + b, '');
                scoresArray.push(stringScore);
            }
            let diagonalScore1 = '';
            let diagonalScore2 = '';
            for(let i in this.gameboard){
                let stringScore = '';
                for(let j in this.gameboard){
                    stringScore += this.gameboard[j][i];
                }
                scoresArray.push(stringScore);
                diagonalScore1 += this.gameboard[i][i];
                diagonalScore2 += this.gameboard[i][3-i];
            }
            scoresArray.push(diagonalScore1);
            scoresArray.push(diagonalScore2);

            if(!this.isGameFinished(scoresArray))
                this.swapPlayer();
        },
        isGameFinished(scoresArray){
            if(scoresArray.includes('xxxx')){
                this.winner = 'X';
            }
            else if(scoresArray.includes('oooo')){
                this.winner = 'o';
            }
            else {
                for(let score of scoresArray){
                    if(score.length < 4)
                        return false;
                }
                alert('empate');
            }
            return true;
        },
        swapPlayer(){
            if(this.activePlayerMarker === 'x')
                this.activePlayerMarker = 'o';
            else
                this.activePlayerMarker = 'x';
        },
        resetGame(){
            this.winner = '';
            this.activePlayerMarker = 'x';
            this.gameboard = [
                ['', '', '', ''],
                ['', '', '', ''],
                ['', '', '', ''],
                ['', '', '', '']
            ];
        }
    },

    components: { Square }
}
</script>