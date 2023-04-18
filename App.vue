<script setup>
  import { ref, computed } from 'vue'

  const questions = ref([
    {
      question: 'Hoano aho hihinanako anao?',
      answer: 1,
      options:  [
        'olona',
        'sakay',
        'voay'

      ],
      selected:null
    },
    {
      question: 'Bibilava mifoka sigara?',
      answer: 2,
      options:  [
        'vilany',
        'kitay',
        'lamasinina'

      ],
      selected:null
    },
    {
      question: 'Loharano antendron-kazo?',
      answer: 2,
      options:  [
        'rano',
        'vorona',
        'voasary'

      ],
      selected:null
    },
    {
      question: 'Tsy misy lohany izy, nefa manao satroka ary misy sofiny?',
      answer: 1,
      options:  [
        'olona',
        'vilany',
        'kitapo'

      ],
      selected:null
    },
    {
      question: 'Anaty rano tsy lena,antanety tsy malazo?',
      answer: 0,
      options:  [
        'aloka',
        'vary',
        'ganagana'

      ],
      selected:null
    },
    {
      question: 'Kitapokelin Andriamanitra tsara zaitra?',
      answer: 0,
      options:  [
        'vary',
        'voasary',
        'kibo'

      ],
      selected:null
    },
    {
      question: 'Eo ambony vavatsika ny tainy?',
      answer: 2,
      options:  [
        'maso',
        'loha',
        'orona'

      ],
      selected:null
    },
    {
      question: 'Aleveno aho haka ny taolako taloha?',
      answer: 2,
      options:  [
        'voanjo',
        'razana',
        'katsaka'

      ],
      selected:null
    },
    {
      question: 'Ilay boka mitaingi-tseza?',
      answer: 0,
      options:  [
        'mananasy',
        'voatavo',
        'zinga'

      ],
      selected:null
    },
    {
      question: 'Izay mivoaka iray maty?',
      answer: 1,
      options:  [
        'miaramila',
        'afokasoka',
        'andro'

      ],
      selected:null
    },
    {
      question: 'Analana vao mihangeza?',
      answer: 1,
      options:  [
        'sakafo',
        'lavaka',
        'mangahazo'

      ],
      selected:null
    },
    {
      question: 'Ampidirina nefa mivoaka ihany?',
      answer: 0,
      options:  [
        'fanjaitra',
        'akoho',
        'akanjo'

      ],
      selected:null
    },
    {
      question: 'Teraka tao anaty rano aho nefa raha mikasi-drano maty?',
      answer: 2,
      options:  [
        'moka',
        'vary',
        'sira'

      ],
      selected:null
    },
    {
      question: 'Ilay mahia miankin-drindrina?',
      answer: 0,
      options:  [
        'kifafa',
        'kitay',
        'olona'

      ],
      selected:null
    }
    
  ])

  const ankCompleted = ref(false)
 
  const currentQuestion = ref(0)
 
  const score = computed (() => {
    let value = 0
    questions.value.map(q  => {
      if (q.selected == q.answer) {
        value++
      }

    })
    return value

  })
 
  const getCurrentQuestion = computed (() => {
    let question = questions.value[currentQuestion.value]
    question.index = currentQuestion.value
    return question
  })
 
  const SetAnswer = evt => {
    questions.value[currentQuestion.value].selected = evt.target.value
    evt.target.value = null
  }
 
  const NextQuestion = () => {
    if (currentQuestion.value < questions.value.length - 1 ) {
      currentQuestion.value++
    } else {
      ankCompleted.value = true
    }
  }
</script>

<template>
  <main class="app">
    <h1>Inona ary izany o!</h1>

    <section class="ank" v-if="!ankCompleted">
      <div class="ank-info">
        <span class="question" > {{ getCurrentQuestion.question  }} </span>
        <span class="score" > Isa {{ score }}/{{ questions.length }} </span> 
      </div>

      <div class="options">
        <label v-for="(option, index) in getCurrentQuestion.options"
        :key="index"
        :class="`option ${
          getCurrentQuestion.selected == index 
           ? index == getCurrentQuestion.answer
            ? 'marina'
            : 'diso'
          :''
        } ${
          getCurrentQuestion.selected!= null && 
          index!= getCurrentQuestion.selected
           ? 'disabled'
           : ''
        }
        `">
          <input type="radio" 
            :name="getCurrentQuestion.index"
            :value="index"
            v-model="getCurrentQuestion.selected"
            :disabled="getCurrentQuestion.selected"
            @change="SetAnswer">
            <span>{{ option }}</span>
        </label>
      </div>
      <button 
      @click="NextQuestion"
      :disabled="!getCurrentQuestion.selected">
      {{
        getCurrentQuestion.index == questions.length - 1
         ? 'tapitra'
         : getCurrentQuestion.selected == null
           ? 'inona ny valiny'
           : 'manaraka' 
      }}

      </button>
    </section>
    <section v-else>
      <div class="farany">
        <h2>Tapitra ny Ankamantatra!</h2>
        <p>Ny isanao dia {{ score }}/{{ questions.length }}</p>
      </div>
    </section>
   
  </main>
</template>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Monserrat', sans-serif;
}
body{
  background-image: url(../65060779_2315663028686715_5578305744542892032_n.jpg);
  background-repeat: no-repeat;
  background-size:inherit;
  background-position: center;
  color: aliceblue;


}
.app{
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 2rem;
  min-height: 100vh;

}
h1{
  font-size: 3rem;
  margin-bottom: 2rem;
  color:rgb(11, 70, 50);
}
.ank{
  background-color: #382a4b;
  padding: 1rem;
  width: 100%;
  max-width: 450px;
  border-radius: 0.5rem;

}
.ank-info{
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;
}
.ank-info >question{

  color: #8F8F8F;
  font-size: 1.25rem; 

}
.options{
  margin-bottom: 1rem;

}
.option{
  padding: 1rem;
  display: block;
  background-color: #271C36;
  margin-bottom: 0.5rem;
  border-radius: 0.5rem;
  cursor: pointer;
}
.option:hover{
  background-color: #2d213f;
}
.option.marina{
  background-color: #2cce7d;
}
.option.diso{
  background-color: #ff5a5f;
}
.option:last-of-type {
  margin-bottom:0;
}
.option.disabled{
  opacity: 0.5;
}
.option input{
  display: none;
}
button{
  appearance: none;
  outline: none;
  border: none;
  cursor: pointer;

  padding: 0,5rem 1rem;
  background-color: #2cce7d;
  color:#2d213f;
  font-weight: 700;
  text-transform: uppercase;
  font-size: 1.25 rem;
  border-radius: 0.5 rem;
}
button:disabled{
  opacity: 0.5;
}
h2{
  font-size: 2rem;
  margin-bottom: 2rem;
  text-align: center;

}
p{
  color:#8F8F8F ;
  font-size: 1.25rem;
  text-align: center;

}
.farany{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Monserrat', sans-serif;

  background-color:darkslateblue ;
  padding: 1rem;
  width: 100%;
  max-width: 450px;
  border-radius: 0.5rem;
}
</style>
