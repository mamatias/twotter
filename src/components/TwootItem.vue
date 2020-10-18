<template>
  <div class="twoot-item">
    <div class="twoot-item__author">
          @{{username}}
    </div>
    <div class="twoot-item__content">
          {{twoot.content}}
    </div>
    <div class="twoot-item__action-bar">
        <div class="twoot-item__action" @click="doRT({id: twoot.id, usr: username})">
            RT
        </div>
        <div class="twoot-item__action" @click="doFAV({id: twoot.id, usr: username})">
            FAV
        </div>
    </div>
  </div>
</template>

<script>
export default {
    name: "TwootItem",
    props : {
        username: {
            type: String,
            required: true
        },
        twoot : {
            type: Object,
            required: true
        }
    },
    methods: {
        doRT(obj){
            this.$emit('rtid', obj);
        },
        doFAV(obj){
            this.$emit('favid', obj);
        }
    }
}
</script>

<style>
.twoot-item {
    background: white;
    border-radius: 5px;
    border: 1px solid rgb(196, 196, 196);
    padding: 3px;
}

.twoot-item__action-bar {
    display: grid;
    grid-template-columns: 1fr 1fr;
}

.twoot-item__action {
    padding: 0.2rem 8px 0px 8px;
    margin-right: auto;
    border-radius: 5px;
    font-weight: bold;
    background: rgb(24, 24, 24);
    color: white;
    cursor: pointer;
}

</style>