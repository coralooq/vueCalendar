<script setup>
    import {ref} from 'vue'

    let date = new Date();
    date.setDate(1);
    let first =  ref(date.getDay());
    let today = ref(new Date().getDate());
    let findFirst = false;
    let count = 1;

    let year = date.getFullYear();
    let month = date.getMonth();

    let last = ref(new Date(year, month + 1, 0).getDate());
    let monthName = ref(date.toLocaleString('default', {month: "long", year: 'numeric'}));

    function prev() {
        date = new Date(year, month - 1);
        date.setDate(1);
        first.value =  date.getDay();
        today.value = new Date().getDate();
        findFirst = false;
        count = 1;

        let localYear = date.getFullYear();
        let localMonth = date.getMonth();
        last.value = new Date(localYear, localMonth + 1, 0).getDate();


        month = date.getMonth();
        year = date.getFullYear();
        
        monthName.value = date.toLocaleString('default', {month: "long", year: 'numeric'});
    };

    function next() {
        date = new Date(year, month + 1);
        date.setDate(1);
        first.value =  date.getDay();
        today.value = new Date().getDate();
        findFirst = false;
        count = 1;

        let localYear = date.getFullYear();
        let localMonth = date.getMonth();
        last.value = new Date(localYear, localMonth + 1, 0).getDate();

        month = date.getMonth();
        year = date.getFullYear();
        
        monthName.value = date.toLocaleString('default', {month: "long", year: 'numeric'});
    }
    
    console.log(first.value)
</script>

<template>
    <div @click='change' id="container">
        <button @click='prev()' id="left">❮</button>
        <input id="data" type="text" :value='monthName' disabled>
        <p class="days"><span>Пн</span><span>Вт</span><span>Ср</span><span>Чт</span><span>Пт</span><span>Сб</span><span>Вс</span></p>
        <table>
            <tr><td v-if='first === 1 && count == today' class='today'>{{count, count++, findFirst = true}}</td><td v-else-if='first === 1'>{{count, count++, findFirst = true}}</td><td v-else></td>  
                <td v-if='first === 2 && count == today' class='today'>{{count, count++, findFirst = true}}</td><td v-else-if='first === 2'>{{count, count++, findFirst = true}}</td><td v-else-if='findFirst && count < last && count == today' class='today'>{{count, count++}}</td><td v-else-if='findFirst && count < last'>{{count, count++}}</td><td v-else></td>  
                <td v-if='first === 3 && count == today' class='today'>{{count, count++, findFirst = true}}</td><td v-else-if='first === 3'>{{count, count++, findFirst = true}}</td><td v-else-if='findFirst && count < last && count == today' class='today'>{{count, count++}}</td><td v-else-if='findFirst && count < last'>{{count, count++}}</td><td v-else></td>  
                <td v-if='first === 4 && count == today' class='today'>{{count, count++, findFirst = true}}</td><td v-else-if='first === 4'>{{count, count++, findFirst = true}}</td><td v-else-if='findFirst && count < last && count == today' class='today'>{{count, count++}}</td><td v-else-if='findFirst && count < last'>{{count, count++}}</td><td v-else></td>  
                <td v-if='first === 5 && count == today' class='today'>{{count, count++, findFirst = true}}</td><td v-else-if='first === 5'>{{count, count++, findFirst = true}}</td><td v-else-if='findFirst && count < last && count == today' class='today'>{{count, count++}}</td><td v-else-if='findFirst && count < last'>{{count, count++}}</td><td v-else></td>  
                <td v-if='first === 6 && count == today' class='today'>{{count, count++, findFirst = true}}</td><td v-else-if='first === 6'>{{count, count++, findFirst = true}}</td><td v-else-if='findFirst && count < last && count == today' class='today'>{{count, count++}}</td><td v-else-if='findFirst && count < last'>{{count, count++}}</td><td v-else></td>  
                <td v-if='first === 0 && count == today' class='today'>{{count, count++, findFirst = true}}</td><td v-else-if='first === 0'>{{count, count++, findFirst = true}}</td><td v-else-if='findFirst && count < last && count == today' class='today'>{{count, count++}}</td><td v-else-if='findFirst && count < last'>{{count, count++}}</td><td v-else></td>
            </tr>
            <tr><template v-for="n in 7"><td v-if='count == today && count < last' class="today">{{count, count++}}</td> <td v-else-if='count < last'>{{count, count++}}</td></template></tr>
            <tr><template v-for="n in 7"><td v-if='count == today && count < last' class="today">{{count, count++}}</td> <td v-else-if='count < last'>{{count, count++}}</td></template></tr>
            <tr><template v-for="n in 7"><td v-if='count == today && count < last' class="today">{{count, count++}}</td> <td v-else-if='count < last'>{{count, count++}}</td></template></tr>
            <tr><template v-for="n in 7"><td v-if='count == today && count <= last' class="today">{{count, count++}}</td> <td v-else-if='count <= last'>{{count, count++}}</td></template></tr>
            <tr><template v-for="n in 7"><td v-if='count == today && count <= last' class="today">{{count, count++}}</td> <td v-else-if='count <= last'>{{count, count++}}</td><td v-else></td></template></tr>
        </table>
        <button @click='next()' id="right">❯</button>
    </div>
    
</template>

<style>
    .today {
        border: 2px solid rgb(252, 231, 203);
    }

    #container {
        display: flex;
        justify-content: center;
        align-items: center;
        position: relative;
        top: 300px;
        height: 155px;
    }

    #left, #right {
        height: 400px;
        width: 40px;
        border: none;
        background-color: rgba(230, 239, 239, 0.3);
        color:grey;
    }

    #left, #right:hover {
        cursor: pointer;
    }

    #data {
        text-align: center;
        font-weight: 600;
        font-size: 18px;
        position: absolute;
        top: -120px;
        width: 378px;
        height: 30px;
        border: none;
        background-color: white;
    }

    td, th {
        width: 50px;
        height: 50px;
        text-align: center;
    }

    .days {
       font-weight: 600;
       position: absolute;
       top: -100px;
       font-size: 17px;
    }

    .days span {
        margin: 0px 17px 0px 17px;
    }

    table {
        position: relative;
        top: 25px;
        max-height: 400px;
    }
</style>