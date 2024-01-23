<!-- the script is where the js code goes -->
<script setup>
import { ref } from "vue"; // you need this to use ref()

// (1) Define a new ref variable within <script setup>and then relate the text to the template using double brackets {{ }}
var username = ref("USER444");

// (2) Create a button with the @click directive that calls back a function within the script. (any function that you can create)
// Timer function

var time = ref(0);
let time_already_running = null;

// Start Timer
function startTimer() {
    if(time_already_running === null){
        time_already_running = setInterval(() => {time.value++;}, 1000)
    }
}

// Stop Timer
function stopTimer(){
    if(time_already_running !== null){
        clearInterval(time_already_running);
        time_already_running = null
    }
}

// Reset Timer
function resetTimer(){
    stopTimer();
    time.value = 0;
}


// (3) Add an input text in the template and a button with @click. Once the button is clicked, it should call back a function that adds the text to a ref variable and display it

var added_Text = ref("No text added so far!");
var input_Text = ref("");

function addText(){
    if(added_Text.value === "No text added so far!"){
        added_Text.value = "";
    }
    added_Text.value = added_Text.value + input_Text.value;

}


// (4) Add two input texts in the sidebar and a button with @click. One will collect a selector and the second one a color. Once youpress the button, it should change the color to that css selector.
var color_selection = ref("");
var element_selection = ref("");

function changeStyle() {
    var element = document.querySelector(element_selection.value);
    element.style.backgroundColor = color_selection.value;
}

</script>



<!-- the template is where the html code goes -->
<template>
   <div id="navbar" class="container">  
        <div id="title">Assignment_02</div>
    </div>

    <div id="flex">

        <div id="sidebar" class="container"> 
            <p>Hello, {{ username }}! Do some stuff!</p>
            <p></p>
            <button @click="startTimer">Start Time</button>
            <button @click="stopTimer">Stop Time</button>
            <button @click="resetTimer">Stop + Reset</button>
            <p></p>
            <input type="text" id="text_box" v-model="input_Text" name="text_box" placeholder="Put your Text here!">
            <button @click="addText">Add Text</button>
            <p></p>
            <input type="text" id="change_color" v-model="color_selection" name="text_box" placeholder="Write Color">
            <input type="text" id="change_element" v-model="element_selection" name="text_box" placeholder="Write Elemente">
            <button @click="changeStyle">Change Style</button>
        </div>

        <div id="main" class="container">
            <p>Time: {{ time }} Seconds</p>
            <p></p>
            <p id="input_Text"> {{ added_Text }}</p>
        </div>
    </div>
</template>



<!-- style is where the css code goes -->
<style scoped>
html{
    
    background-color: rgb(59, 59, 59); 
    color: white;
}

body{
    margin:0;
}

div{
    box-sizing: border-box;
}

img{
    height: 100%;
    width: auto;
}

#navbar{
    height: 50px;
    border-color: red;
    display: flex; 
    justify-content: center;
    align-items: center;
    font-size: larger;
    font-weight: bold;
}

#flex{
    display: flex;
    height: calc(100vh - 50px);
}

#sidebar{
    width:30%;
    border-color: blue;
}

#main{
    width:70%;
    border-color: green;
}

#title{
}

button{
    margin-left: 10px;
}

.container{
    border-style: dotted;
    border-width: 1px;
}
</style>