<template>
  <div>
    <form>
      <b-select id="term-selector" v-model="selectedSemester"
                size="is-medium"
                @input="newSemesterSelected">
        <option v-for="semester in semesters"
                :value="semester.value">
          {{ semester.text }}
        </option>
      </b-select>
      <div style="height: 25px;">
        
      </div>
      <b-select id="type-selector" v-model="selectedType" @input="newTypeSelected" size="is-medium">
        <option v-for="type in types" :value="type.value">
          {{ type.text }}
        </option>
      </b-select>
      <b-switch id="night-mode-switch" size="is-medium" v-model="nightMode" @input="newModeSelected"><p id="night-mode-text">Night Mode</p></b-switch>
    </form>
  </div>
</template>

<script>
export default {
  name: 'semester-selector',
  data() {
    return {
      selectedType: 'class',
      types: [
        { text: 'Class', value: 'class' },
        { text: 'Lab', value: 'lab' },
        { text: 'Independent Study', value: 'IS' },
        { text: 'Independent Research', value: 'IR' },
        { text: 'Academic Internship', value: 'AI' },
      ],
      nightMode: 0,
      semesters: [
        { text: 'Fall', value: 1 },
        { text: 'Interim', value: 2 },
        { text: 'Spring', value: 3 },
        { text: 'Summer Session 1', value: 4 },
        { text: 'Summer Session 2', value: 5 },
      ],
      selectedSemester: 1,
      navbar: [
        "linear-gradient(315deg, #ff4e00 0%, #ec9f05 74%)",
        "linear-gradient(315deg, #abe9cd 0%, #3eadcf 74%)",
        "linear-gradient(150deg, #ff8177 0%, #ff867a 0%, #ff8c7f 21%, #f99185 52%, #cf556c 78%, #b12a5b 100%)",
        "transparent",
        "transparent",
        "transparent",
      ],
      header: [
        "linear-gradient(315deg, #ff4e00 0%, #ec9f05 74%)",
        "linear-gradient(315deg, #abe9cd 0%, #3eadcf 74%)",
        "linear-gradient(150deg, #ff8177 0%, #ff867a 0%, #ff8c7f 21%, #f99185 52%, #cf556c 78%, #b12a5b 100%)",
        "transparent",
        "transparent",
        "transparent",
      ],
      myCourses: [
        "linear-gradient(315deg, #ff4e00 0%, #ec9f05 74%)",
        "linear-gradient(315deg, #abe9cd 0%, #3eadcf 74%)",
        "linear-gradient(150deg, #ff8177 0%, #ff867a 0%, #ff8c7f 21%, #f99185 52%, #cf556c 78%, #b12a5b 100%)",
        "transparent",
        "transparent",
        "transparent",
      ],
        // "linear-gradient(315deg, #ff4e00 0%, #ec9f05 74%)",
        // "#ec9f05",
        // "linear-gradient(150deg, #ff8177 0%, #ff867a 0%, #ff8c7f 21%, #f99185 52%, #cf556c 78%, #b12a5b 100%)", 
      tables1: [
        "hsl(41, 100%, 46%)",
        "#3eadcf",
        "#e68875",
        "transparent",
        "transparent",
        "transparent",
      ],
      stolafCourses: [
        "linear-gradient(315deg, #ff4e00 0%, #ec9f05 74%)",
        "linear-gradient(315deg, #abe9cd 0%, #3eadcf 74%)",
        "linear-gradient(150deg, #ff8177 0%, #ff867a 0%, #ff8c7f 21%, #f99185 52%, #cf556c 78%, #b12a5b 100%)",
        "transparent",
        "transparent",
        "transparent",
      ],
      pagination: [
        "linear-gradient(315deg, #ff4e00 0%, #ec9f05 74%)",
        "linear-gradient(315deg, #abe9cd 0%, #3eadcf 74%)",
        "linear-gradient(150deg, #ff8177 0%, #ff867a 0%, #ff8c7f 21%, #f99185 52%, #cf556c 78%, #b12a5b 100%)",
        "transparent",
        "transparent",
        "transparent",
      ],
        // "#FFA500",
      tables2: [
        "linear-gradient(315deg, #ff8000 0%, #ec9f05 74%)",
        "linear-gradient(to bottom, #3eadcf, #3eadcf, #3eadcf, #3eadcf, #3eadcf)",
        "linear-gradient(to bottom, #ff8177, #fe857a, #fc897e, #fb8d81, #f99185)",
        "transparent",
        "transparent",
        "transparent",
      ],
      contact: [
        "linear-gradient(315deg, #ff4e00 0%, #ec9f05 74%)",
        "linear-gradient(315deg, #abe9cd 0%, #3eadcf 74%)",
        "linear-gradient(150deg, #ff8177 0%, #ff867a 0%, #ff8c7f 21%, #f99185 52%, #cf556c 78%, #b12a5b 100%)",
        "transparent",
        "transparent",
        "transparent",
      ],
      actionBtnClasses: [
        'fall-btn',
        'interim-btn',
        'spring-btn',
        'summer1-btn',
        'summer2-btn',
        'night-mode-btn'
      ],
      backgroundImages: [
        'fall-img',
        'winter-img',
        'spring-img',
        'summer-one-img',
        'summer-two-img',
        'night-mode-img',
      ]
    }
  },
  mounted() {
    this.nightMode = window.innerWidth <= 500;
    this.changeSeasonTheme(1)
  },
  methods: {
    newModeSelected() {
      this.nightMode ? this.changeSeasonTheme(5) : this.changeSeasonTheme(this.selectedSemester)
      this.$emit('newModeSelected', this.nightMode)
    },
    newTypeSelected() {
      this.$emit('newTypeSelected', 'type' ,this.selectedType)
    },
    newSemesterSelected() {
      this.$emit('newSemesterSelected', 'semester' , this.selectedSemester)
      this.changeSeasonTheme(this.selectedSemester)
    },
    changeElementsStyle(elements, styleName, styling) {
      for(var i = 0; i < elements.length; i++) {
        elements[i].style[styleName] = styling
        elements[i].style[styleName] = styling
      }
    },
    changeSeasonTheme(semester) {
      if(this.nightMode) {
        semester = 6
      }

      // Get Elements
      var app = document.getElementById('app')
      var tables = document.getElementsByTagName('table')
      var tableTop = document.getElementsByClassName('vgt-global-search')[0]
      var stolafCourses = document.getElementById('stolaf-courses-table-options')
      var contact = document.getElementById('contact')
      var upArrowCircle = document.getElementById('up-arrow-circle')
      var tableColumns = document.getElementsByClassName("table-columns")
      var tableRows = document.getElementsByClassName("my-row")
      var vgtSelect = document.getElementsByClassName("vgt-select")
      var vgtInput = document.getElementsByClassName("vgt-input")
      var stolafCoursesFooter = document.getElementById('stolaf-courses-footer')


      semester -= 1

      // Set style of elements 
      tables[0].style.background = this.tables1[semester]
      tableTop.style.background = this.contact[semester]
      stolafCourses.style.background = this.stolafCourses[semester]
      contact.style.background = this.contact[semester]
      upArrowCircle.style.background = this.contact[semester]
      stolafCoursesFooter.style.background = this.contact[semester]


      if(this.nightMode) {
        this.changeElementsStyle(vgtSelect, 'backgroundColor', '#BEBEBE')
        this.changeElementsStyle(vgtInput, 'background', '#BEBEBE')
        this.changeElementsStyle(vgtSelect, 'color', 'black')
        this.changeElementsStyle(vgtInput, 'color', 'black')
        this.changeElementsStyle(tableColumns, 'color', '#BEBEBE')
        this.changeElementsStyle(tableRows, 'color', '#BEBEBE')
      } else {
        this.changeElementsStyle(vgtSelect, 'backgroundColor', 'white')
        this.changeElementsStyle(vgtInput, 'background', 'white')
        this.changeElementsStyle(tableColumns, 'color', 'white')
        this.changeElementsStyle(tableRows, 'color', 'white')
        this.changeElementsStyle(vgtSelect, 'color', '#606266')
        this.changeElementsStyle(vgtInput, 'color', '#606266')
      }

      // Set classes of elements
      // this.addSeasonClass(semester, stolafActionBtns[0], this.actionBtnClasses)
      // this.addSeasonClass(semester, stolafActionBtns[1], this.actionBtnClasses)
      // this.addSeasonClass(semester, showBtn, this.actionBtnClasses)
      // this.addSeasonClass(semester, userActionBtns[0], this.actionBtnClasses)
      // this.addSeasonClass(semester, userActionBtns[1], this.actionBtnClasses)

      this.addSeasonClass(semester, app, this.backgroundImages)
    },
    addSeasonClass(semester, element, listOfClasses) {
      listOfClasses.forEach(season => {
        if (element.classList.contains(season)) {
          element.classList.remove(season); 
        }
      })
      element.classList.add(listOfClasses[semester])
    },
  }
}
</script>

<style>

/*#night-mode-switch {
  visibility: hidden;
}*/

@media screen and (max-width: 400px) {
  #night-mode-switch {
    visibility: hidden;
  }
}

#term-selector {
  margin-bottom: 25px;
}

#night-mode-switch {
  margin-top: 25px;
}

.grey-font {
  color: #BEBEBE !important;
}

#night-mode-text {
  font-weight: 500;
  color: white;
}

.fall-btn {
  background: linear-gradient(315deg, #ff4e00 0%, #ec9f05 74%)
}
.interim-btn {
  background: linear-gradient(315deg, #abe9cd 0%, #3eadcf 74%);
}
.spring-btn {
  background: linear-gradient(150deg, #ff8177 0%, #ff867a 0%, #ff8c7f 21%, #f99185 52%, #cf556c 78%, #b12a5b 100%);
}
.summer1-btn {
  background: linear-gradient(147deg, #000000 0%, #04619f 74%);
  background-image: linear-gradient(147deg, #000000 0%, #04619f 74%) !important;
}
.summer2-btn {
  border: 1px solid black;
  background-color: #6c33a3;
  background-image: linear-gradient(316deg, #6c33a3 0%, #8241b8 74%);
}

.night-mode-btn {
  background: #BEBEBE;
}

.summer-one-img {
  background-image: linear-gradient(147deg, #000000 0%, #04619f 74%) !important;
}

.summer-two-img {
  background-color: #6c33a3;
  background-image: linear-gradient(316deg, #6c33a3 0%, #8241b8 74%) !important;
}

.night-mode-img {
  background: black !important;
}

.spring-img {
   background: url(../assets/spring-img.jpg) no-repeat center center fixed!important
}

.winter-img {
  background: url('../assets/winter-img.jpg') no-repeat center center fixed !important;
}

.fall-img {
  background: url('../assets/fall-img.jpg') no-repeat center center fixed !important; 
}

</style>