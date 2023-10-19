<template>
    <div>
        <hr>
        Восьме завдання
        <br>
        <ul v-for="(item, index) in list" :key="index">
            <li>
                {{ item.title }}
            </li>
            <ul v-for="(subItem, subIndex) in item.subList" :key="subIndex">
                <li>
                    {{ subItem }}
                </li>
            </ul>
        </ul>
        <hr>
        Девяте/Десяте завдання
        <br>
        <ul>
            <template v-for="(p, index) in paginatedData">

                <li :key="index" v-if="filtered(index)">
                    {{ p.first }}
                    {{ p.last }}
                    {{ p.suffix }}
                </li>
            </template>
        </ul>
        <button :disabled="pageNumber === 0" @click="prevPage">
            Previous
        </button>
        <button :disabled="pageNumber >= pageCount - 1" @click="nextPage">
            Next
        </button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            list: [
                {
                    title: 'Список покупок №1',
                    subList: ['Картошка', 'Хлеб', 'Чай']
                },
                {
                    title: 'Список покупок №2',
                    subList: ['Печенье', 'Мясо', 'Овощи']
                },
                {
                    title: 'Список покупок №3',
                    subList: ['Банан', 'Клубника', 'Арбуз']
                }
            ],
            pageNumber: 0,
            listData: '',
            size: 10

        }
    },
    created() {
        this.listData = this.createFakeData();
    },
    methods: {
        createFakeData() {
            let data = [];
            for (let i = 0; i < 100; i++) {
                data.push({
                    first: 'Myhlovets',
                    last: 'Vladyslav',
                    suffix: '№' + parseFloat(i + 1)
                });
            }
            return data;
        },
        nextPage() {
            this.pageNumber++;
        },
        prevPage() {
            this.pageNumber--;
        },
        filtered(index) {
            return index % 2 !== 0
        }
    },
    computed: {
        paginatedData() {
            const start = this.pageNumber * this.size,
                end = start + this.size;
            return this.listData.slice(start, end);
        },
        pageCount() {
            let l = this.listData.length,
                s = this.size;
            return Math.ceil(l / s);

        },
    }
}
</script>