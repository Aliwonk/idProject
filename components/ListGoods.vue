<template>
    <div class="listGood">
        <div class="head">
            <div class="filter">
                <select>
                    <option value="default">По умолчанию</option>
                    <option value="min">Мин</option>
                    <option value="max">Макс</option>
                </select>
            </div>
        </div>

        <div class="list">
            <div 
                class="goodCard"
                @mouseenter="showDelBtn" 
                @mouseleave="hideDelBtn"
                v-for="good in goods"
                :key="good.id"
            >
                <div 
                    class="btnDel btnDelHide"
                    @click="delGood"
                ></div>
                <NuxtLink
                    :to="'/good/' + good.id"
                >
                    <img src='../assets/img/stolb_tablichka_nadpis_119232_3840x2400.jpg' alt="">
                    <div class="infoGood">
                        <div class="nameGood">{{ good.nameGood }}</div>
                        <div class="descGood">{{ good.descGood }}</div>
                        <div class="priceGood">{{ good.priceGood }}</div> 
                    </div>
                </NuxtLink>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            goods: [
                { 
                    id: 1,
                    linkImg: '../assets/img/stolb_tablichka_nadpis_119232_3840x2400.jpg',
                    nameGood: 'Наименование товара',
                    descGood: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
                    priceGood: '12 000 руб.'
                },
                { 
                    id: 2,
                    linkImg: '../assets/img/stolb_tablichka_nadpis_119232_3840x2400.jpg',
                    nameGood: 'Наименование товара',
                    descGood: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
                    priceGood: '12 000 руб.'
                }
            ]
        }
    },
    methods: {
        delGood(event) {
            const goodCard = event.target.parentElement;
            goodCard.remove();
        },
        showDelBtn(event) {
            const btnDel = event.target.firstChild;
            btnDel.classList.remove('btnDelHide');
        },
        hideDelBtn(event) {
            const btnDel = event.target.firstChild;
            btnDel.classList.add('btnDelHide');
        }
    }
}

</script>

<style scoped>
.listGood{
    display: block;
    width: 90%;
    height: 100vh;
    margin-top: 32px;
    overflow: auto;
}
.listGood::-webkit-scrollbar{
    width: 0px;
}
.listGood .head{
    display: flex;
    justify-content: flex-end;
    width: 93%;
    height: 36px;
    margin-bottom: 16px;
}
.head .filter{
    display: flex;
    align-items: center;
    justify-content: center;
    width: 120px;
    height: 36px;
    background-color: #FFFEFB;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
}

.filter select {
    text-align: center;
    border: none;
    outline: none;
    user-select: none;
}


.listGood .list{
    display: flex;
    flex-direction: row;
    justify-content: center;
    flex-wrap: wrap;
    width: 100%;
    height: inherit;
} 
.list .goodCard{
    display: flex;
    flex-direction: column;
    width: 332px;
    height: 423px;
    margin-left: 16px;
    margin-bottom: 16px;
    border-radius: 4px;
    transition: .3s;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    cursor: pointer;
}

.goodCard .btnDel{
    display: flex;
    justify-content: center;
    align-items: center;
    width: 32px;
    height: 32px;
    margin-bottom: -22px;
    margin-left: 91%;
    background-color: #FF8484;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    z-index: 100;
    cursor: pointer;
    transition: .2s;
    background-image: url('../assets/icon/Vector.svg');
    background-position: center center;
    background-repeat: no-repeat;
}

.btnDel:hover{
    transform: rotate(15deg);
}

.btnDelHide{
    opacity: 0;
}

.goodCard a {
    width: 100%;
    height: 100%;
}

.goodCard img{
    width: 100%;
    height: 45%;
}

.goodCard:hover{
    transform: translateX(-1px);
    border: none;
    box-shadow: 0px 20px 30px rgb(0 0 0 / 20%), 0px 6px 10px rgba(0, 0, 0, 0.02);
}

.goodCard .infoGood{
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    width: 90%;
    height: 50%;
    padding-left: 16px;
    padding-right: 16px;
    color: #3F3F3F;
}

.infoGood .nameGood{
    font-weight: 600;
    font-size: 20px;
    line-height: 25px;
}

.infoGood .descGood{
    font-weight: 400;
    font-size: 16px;
    line-height: 20px;
}

.infoGood .priceGood{
    font-weight: 600;
    font-size: 24px;
    line-height: 30px;
}
</style>