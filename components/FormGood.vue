<template>
    <div class="blockCreateGood">
        <div class="caption">Добавление товара</div>

        <form method="post">
            
            <div class="itemForm">
                <label for="nameGood">
                    Наименование товара
                    <div class="dotted"></div>
                </label>
                <input 
                    type="text" 
                    v-model="nameGood" 
                    id="nameGood"
                    name="nameGood"
                    @keydown="clearValue"
                    @input="onChange"
                    placeholder="Введите наименование товара"
                >
                <span 
                    class="messageError" 
                    v-if="required.nameGood"
                >Поле является обязательным</span>
            </div>
            
            <div class="itemForm">
                <label for="descGood">Описание товара</label>
                <textarea 
                    v-model="descGood" 
                    id="descGood" 
                    name="descGood"
                    placeholder="Введите описание товара"
                ></textarea>
            </div>
            

            <div class="itemForm">
                <label for="linkImg">
                    Ссылка на изображение товара
                    <div class="dotted"></div>
                </label>
                <input 
                    type="text" 
                    v-model="linkImg" 
                    id="linkImg"
                    name="linkImg"
                    @input="onChange"
                    @keydown="clearValue"
                    placeholder="Введите ссылку"
                >
                <span 
                    class="messageError" 
                    v-if="required.linkImg"
                >Поле является обязательным</span>
            </div>

            <div class="itemForm">
                <label for="priceGood">
                    Цена товара
                    <div class="dotted"></div>
                </label>
                <input 
                    type="number" 
                    v-model="priceGood"
                    id="priceGood"
                    name="priceGood"
                    @keydown="clearValue"
                    @input="onChange"
                    placeholder="Введите цену"
                >
                <span 
                    class="messageError" 
                    v-if="required.priceGood"
                >Поле является обязательным</span>
            </div>
            <button @click="onSubmit" class="btnAdd" :class="{ unactive }" >Добавить товар</button>
        </form>
    </div>
</template>

<script>
export default {
    data() {
        return {
            nameGood: '',
            descGood: '',
            linkImg: '',
            priceGood: '',
            required: {
                nameGood: false,
                priceGood: false,
                linkImg: false
            },
            unactive: true
        }
    },
    methods: {
        clearValue(event) {
            const input = event.target;
            const idInput = input.id;

            this.required[idInput] = false;

            input.classList.forEach(className => {
                if(className === 'errorValid') {
                    input.classList.remove('errorValid');
                    input.value = '';
                }
            });
        },
        onChange() {
            if(
                this.nameGood !== '' &&
                this.linkImg !== '' &&
                this.priceGood !== ''
            ){
                this.unactive = false
            }
        },
        validateData(inputs) {
            if(
                this.nameGood === '' &&
                this.linkImg === '' &&
                this.priceGood === ''
            ){

                inputs.nameGood.classList.add('errorValid');
                inputs.linkImg.classList.add('errorValid');
                inputs.priceGood.classList.add('errorValid');

                this.required.nameGood = true;
                this.required.linkImg = true;
                this.required.priceGood = true

                return false;

            } else if(this.nameGood === '') {

                inputs.nameGood.classList.add('errorValid');
                this.required.nameGood = true;

                return false;

            } else if(this.linkImg === '') {

                inputs.linkImg.classList.add('errorValid');
                this.required.linkImg = true;
                
                return false;

            } else if(this.priceGood === '') {

                inputs.priceGood.classList.add('errorValid');
                this.required.priceGood = true;
                
                return false;

            } else {

                return true;

            }

        },

        onSubmit(event) {
            event.preventDefault();
            const inputs = event.target.form.elements;
            const valid = this.validateData(inputs);
            
            if(valid) {
                console.log('send')
            }

        }
    },
}

</script>

<style scoped>
.blockCreateGood{
    display: flex;
    flex-direction: column;
    width: 364px;
    height: auto;
    padding-left: 32px;
    padding-top: 32px;
}

.caption{
    font-style: normal;
    font-weight: 600;
    font-size: 28px;
    line-height: 35px;
}

.blockCreateGood form {
    display: flex;
    flex-direction: column;
    padding: 24px;
}
.blockCreateGood form input, textarea, button {
    width: inherit;
    height: 36px;
    padding-left: 16px;
    background: #FFFEFB;
    border-radius: 4px;
    outline: none;
    border: none;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
}

.blockCreateGood form textarea {
    height: 108px;
    padding-top: 10px;
}

.blockCreateGood form label {
    display: flex;
    flex-direction: row;
    margin-bottom: 4px;
    font-style: normal;
    font-weight: 600;
    font-size: 12px;
    line-height: 13px;
    letter-spacing: -0.02em;
    color: #49485E;
}

.itemForm{
    width: 100%;
    height: auto;
    margin-bottom: 16px;
}


.dotted{
    width: 4px;
    height: 4px;
    background-color: #FF8484;
    border-radius: 4px;
}

form input[class='errorValid'] {
    border: 1px solid #FF8484;
}

.messageError{
    color: #FF8484;
    font-size: 12px;
}

.btnAdd{
    background-color: #3c6137;
    color: #FFFFFF;
    cursor: pointer;
    transition: 0.3s;
}

.unactive{
    background-color: #EEEEEE;
    color: #B4B4B4;
    cursor: default;        
}
</style>