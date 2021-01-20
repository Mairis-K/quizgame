<template>
  <div class="container-app">
        <div class="container-quiz">
          <div class="header-quiz">
            <h1>Country Quiz App</h1>
          </div>
          <div class="step-progress" :style="{'width':progress + '%'}"></div>
          <div class="box" v-for="(question,index) in questions.slice(a,b)" :key="index" v-show="quiz">
              <div class="box-question">
                <h2>Question {{b}}/{{questions.length}}</h2>
                <p>{{question.question}}</p>
              </div>
              <div class="box-propositions">
                <ul>
                  <li v-for="(proposition,index) in question.propositions" :key="index" class="li" @click="selectResponse(proposition,index)" :class=" correct ? check(proposition) : ''">{{proposition.props}} <div class="fas fa-check" v-if="correct ?  proposition.correct: ''"></div><div class="fas fa-times" v-if="correct ?  !proposition.correct: ''"></div></li>
                </ul>
              </div>             
          </div>
          <div class="box-score" v-if="score_show">
              <h2>Your score: </h2>
              <h2>{{score}}/{{questions.length}}</h2>
              <div class="btn-restart">
                  <button @click="restartQuiz">Restart game<i class="fas fa-sync-alt"></i></button>
              </div>
          </div>
          <div class="footer-quiz">
                <div v-if="progress < 100" class="box-button">
                    <button  @click="skipQuestion()" :style="next ? 'background-color: rgb(106, 128, 202)' : ''">Skip</button>
                    <button  @click="nextQuestion()" :style="!next ? 'background-color: rgb(106, 128, 202)' : ''">Next</button>
                </div>  
          </div>
        </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      questions:[
        {
          question:"Witch of these is the largest landlocked country in the world?",
          propositions:[
            {props:'Kazakhstan',correct:true},
            {props:'Bolivia'},
            {props:'Paraguay',},
            {props:'Central African Republic',}
          ]
        },
        {
          question:"What country has the largest Muslim population?",
          propositions:[
            {props:'Nigeria',},
            {props:'Iraq',},
            {props:'Indonesia',correct:true},
            {props:'Libya'},
          ]
        },
        {
          question:"What European country is divided into departments?",
          propositions:[
            {props:'Sweden'},
            {props:'Switzerland'},
            {props:'France',correct:true},
            {props:'Germany'},
          ]
          
        },
        {
          question:"Which of these countries is said to be shaped like an elephant’s head?",
          propositions:[
            {props:'France',},
            {props:'Thailand',correct:true},
            {props:'Australia',},
            {props:'Zaire',},
          ]
        },
        {
          question:"In what country might one hear the song Waltzing Matilda frequently played?",
          propositions:[
            {props:'Congo',},
            {props:'Brazil'},
            {props:'Paraguay'},
            {props:'Australia',correct:true},
          ]
        },
      ],
      a:0,
      b:1,
      next:true,
      score_show:false,
      quiz:true,
      score:0,
      correct:false,
      progress:0,
    }
  },
  name: 'App',
  components: {
  },
  computed:{
  },
  methods:{
    selectResponse(e){
      this.correct = true;
      this.next = false;
      if (e.correct) {
        this.score++;
      }
    },
    check(status){
        if (status.correct) {
          return 'correct'
        }else{
          return 'incorrect' 
        }
    },
    nextQuestion(){
      if (this.next) {
        return;
      }
      this.progress = this.progress + (100/this.questions.length);
      if(this.questions.length - 1 == this.a){
        this.score_show = true;
        this.quiz = false;    
      }
      else{
        this.a++;
        this.b++;
        this.correct = false;
        this.next = true;
      }
    },
    skipQuestion(){
      if (!this.next) {
        return;
      }
      this.progress = this.progress + (100/this.questions.length);
      if(this.questions.length - 1 == this.a){
        this.score_show = true;
        this.quiz = false;
      }else{
        this.a++;
        this.b++;
      }
    },
    restartQuiz(){
      Object.assign(this.$data, this.$options.data());
    },
  }
}
</script>


