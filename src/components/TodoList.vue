<template>
    <div class="TodoList">
        <div class="container">
            <div class="container-title">
                <img src='../assets/todolist-logo.png'>
                <h1>Список задач</h1>
                <LikeBtn></LikeBtn>
            </div>
            <div class="container-body">
                <div class="wrapper">
                    <div class="list">
                        <div class="item" :class="{ done: task.done }" v-for="task in tasks" :key="task.text.tasks">
                            <input type="checkbox" v-model="task.done">
                            {{ task.text }} <LikeBtn></LikeBtn>
                        </div>
                    </div>
                    <div class="form">
                        <input class="input input-add-task" v-model="message" v-on:keyup.enter="addTask" placeholder="Введите текст...">
                        <button class="btn btn-add-task" type="button" @click="addTask">Добавить</button>
                    </div>
                    <!-- Есть 2 метода скрыть/показать элементы на стр: через циклы или через v-show (остается в DOM благодря display: none;) -->
                    <div class="message-count-task">
                        <div class="message-info message-tasks-done" v-if="count() == 0">Все задания выполнены!</div>
                        <div class="message-info" v-else-if="count() == 1">Осталась одна задача</div>
                        <div class="message-info" v-else>Осталось сделать задач: <span class="counter">{{ count() }}</span></div>
                        <img class="img-tasks-done" src="https://pngimage.net/wp-content/uploads/2018/06/yes-emoji-png-4.png" alt="" v-show="count() == 0">
                    </div>
<!--                    <div class="author">-->
<!--                        <span>by T. Kharitonov</span>-->
<!--                        <div class="social">-->
<!--                            <a href="https://github.com/bykharitonoff"><img src="../assets/github.svg" alt=""></a>-->
<!--                            <a href="https://t.me/bytim"><img src="../assets/telegram.svg" alt=""></a>-->
<!--                        </div>-->
<!--                    </div>-->
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import LikeBtn from './LikeBtn.vue'

    export default {
        name: "TodoList",
        components: {
            LikeBtn
        },
        data() {
            return {
                message: '',
                tasks: [
                    {text: 'Развернуть проект', done: true},
                    {text: 'Создать todo-list', done: true},
                    {text: 'Стилизовать', done: false}
                ]
            }
        },
        methods: {
             addTask() {
                 this.tasks.push({
                     text: this.message,
                     done: false
                 });
                 this.message = ''
             },
            count() {
                 return this.tasks.filter(task => !task.done).length;
            }
        }
    }
</script>

<style scoped>
    input:focus {
        outline: none;
    }
    .list {
        padding: 20px 40px;
        border: 1px solid #ccc;
        margin: 20px 0;
        text-align: left;
        font-size: 14px;
        max-height: 50vh;
        overflow: scroll;
    }
    .item {
        margin: 10px 0;
        display: flex;
        align-items: center;
    }
    .item input {
        margin-right: 5px;
    }
    .form {
        margin: 20px 0 7px 0;
    }
    .done {
        text-decoration: line-through;
    }
    .img-tasks-done {
        width: 25px;
    }
    .wrapper {
        width: 767px;
        margin: 0 auto;
        padding: 0 20px;
    }
    .container-title {
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .container-title img {
        width: 40px;
        margin-right: 20px;
    }
    .message-count-task {
        display: flex;
        justify-content: center;
        align-items: flex-end;
    }
    .message-info {
        font-style: italic;
        font-size: 14px;
    }
    .message-info.message-tasks-done {
        font-style: normal;
        font-weight: bold;
        font-size: 16px;
    }
    .message-info .counter {
        font-style: normal;
        font-weight: bold;
    }
    .input-add-task {
        border: 1px solid #ccc;
        border-right: 0;
        padding: 5px;
        border-radius: 5px 0 0 5px;
        min-width: 25%;
    }
    .btn {
        border-radius: 0 5px 5px 0;
    }
    .btn-add-task {
        background: #0097ff;
        color: #fff;
        padding: 6px 12px;
        border: 0;
        cursor: pointer;
    }
    .btn-add-task:hover {
        background: #1582ce;
    }
    .author {
        padding: 35px 0;
        display: flex;
        flex-direction: column;
        justify-content: flex-end;
        align-items: flex-end;
        font-style: italic;
        font-size: 12px;
    }
    .social {
        display: flex;
    }
    .social a {
        margin-top: 5px;
        margin-left: 5px;
    }
    .social img {
        width: 20px;
        filter: grayscale(90%);
    }
    .social img:hover {
        filter: grayscale(0%);
    }

    @media only screen and (max-width: 1024px) {
        .wrapper {
            width: auto;
        }
        #app {
            margin-top: 20px;
        }
    }
</style>