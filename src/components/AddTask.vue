<template>
    <form class="add-form" @submit="onSubmit">
        <div class="form-control">
            <label for="">Заметка</label>
            <input type="text" v-model="text" name="text" placeholder="Добавит заметку...">
        </div>
        <div class="form-control">
            <label for="">Дата & Время</label>
            <input type="text" v-model="day" name="day" placeholder="Добавит Дата & Время...">
        </div>
        <div class="form-control form-control-check">
            <label for="">Отметить</label>
            <input type="checkbox" v-model="reminder" value="reminder">
        </div>
        <input type="submit" @click="onPush" value="Save Task" class="btn btn-block">
    </form>
</template>

<script>
export default {
    name: 'AddTask',
    data() {
        return {
            text: '',
            day: '',
            reminder: false
        }
    },
    methods: {
        onSubmit(e) {
            e.preventDefault()

            if(!this.text) {
                alert("You are not writing!")
            }

            const newTask = {
                id: Math.floor(Math.random() * 20040916),
                text: this.text,
                day: this.day,
                reminder: this.reminder
            }

            if(this.text && this.day) {
                this.$emit('add-task', newTask);
            }else {
                alert("Unfortunately, we cannot found your message!")
            }
            this.text = '';
            this.day = '';
            this.reminder = false;
        }
    }
}
</script>

<style scoped>
.add-form {
    margin-bottom: 40px;
}
.form-control {
    margin: 20px 0;
}
.form-control label {
    display: block;
}
.form-control input {
    width: 100%;
    height: 40px;
    margin: 5px;
    padding: 3px 7px;
    font-size: 17px;
}
.form-control-check {
    display: flex;
    align-items: center;
    justify-content: space-evenly;
}
.form-control-check label {
    flex: 1;
}
.form-control-check input {
    flex: 2;
    height: 20px;
}


</style>