<template>
    <div class="popup" v-bind:class="{ popupopen: isPlaying }">
         <div class="rule">
             <h3 style="padding:8px 8px;">Luật chơi</h3>
             <p style="padding:8px 8px;">Lorem ipsum dolor sit, amet consectetur adipisicing elit. Asperiores nemo perspiciatis recusandae porro iste eligendi excepturi ex, possimus adipisci sint earum numquam dolores, neque error itaque fugit nesciunt molestias exercitationem.</p> 
             <button class="confirm" v-on:click="handleConfirm()">Đã hiểu</button>
         </div>
    </div>
</template>

<script>
    export default {
        name : 'popup',
        data(){
            return {

            }
        },
        props : {
            isPlaying : { type:Boolean, default: false }
        },
        methods : {
            handleConfirm(){
                this.$emit('confirm');
            }
        }
    }
</script>

<style scoped>
.popup{
    opacity: 0;
    visibility: hidden;
}

.popupopen{
    opacity: 1;
    visibility: visible;
    width: 100%;
    height: 667px;
    background-color: rgb(0 0 0 / 20%);
    position: relative;
    top: 0;
    left: 0;
    z-index: 50;
    display: flex;
    flex-direction: column;
    justify-content: center;
}


.popupopen .rule{
    background-color: aliceblue;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}
.popupopen .rule .confirm{
    width: 50%;
    background-color: aliceblue;
    color: black;
    margin-left: 2%;
    padding: 8px 8px;
    transition:  all .3s ease;
    margin-bottom: 10px;
}
.popupopen .rule .confirm:hover{
    background-color: black;
    color: aliceblue;
    cursor: pointer;
}
</style>