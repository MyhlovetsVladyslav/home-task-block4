<template>
    <div>
        <hr>
        Перше/Четверте/П'яте завдання
        <button @click="getAll">Кнопка</button>
        <ul>
            <li v-for="(clickTime, index) in clickTime" :key="index" :class="'slide-in slide-in-' + animations[index]"
                :style="{ backgroundColor: randomColors[index], fontSize: randomFontSizes[index] + 'px' }">
                Клікнуто: {{ clickTime }}
            </li>
        </ul>
        <hr>
    </div>
</template>
  
<script>

export default {
    data() {
        return {
            clickTime: [],
            randomColors: [],
            randomFontSizes: [],
            animations: [],
        }
    },
    methods: {
        getAll() {
            this.saveClick()
            this.getRandomColor()
            this.getRandomFontSize()
            this.getRandomAnimation()
        },
        saveClick() {
            const currentTime = new Date().toLocaleTimeString();
            this.clickTime.push(currentTime);
        },
        getRandomColor() {
            let letters = '0123456789ABCDEF';
            for (let i = 0; i < this.clickTime.length; i++) {
                let color = '#';
                for (let j = 0; j < 6; j++) {
                    color += letters[Math.floor(Math.random() * 16)];
                }
                this.randomColors.push(color);
            }
        },
        getRandomFontSize() {
            let number = Math.floor(Math.random() * (36 - 12 + 1)) + 12;
            this.randomFontSizes.push(number)
        },
        getRandomAnimation() {
            let li = Math.floor(Math.random() * 4) + 1;
            this.animations.push(li)
        }

    },
}
</script>
  
<style scoped>
.slide-in-1 {
    animation: slide-in 1s ease forwards;
}

.slide-in-2 {
    animation: slide-in 2s ease forwards;
}

.slide-in-3 {
    animation: slide-in 3s ease forwards;
}

.slide-in-4 {
    animation: slide-in 4s ease forwards;
}

@keyframes slide-in {
    0% {
        transform: translateX(-100%);
    }

    100% {
        transform: translateX(0);
    }
}
</style>
  