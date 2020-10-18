<template>
    <div class="user-profile">
        <div class="user-profile__user-panel">
            <h1 class="user-profile__user-name">@{{user.username}}</h1>
            <div class="user-profile__admin-badge" v-if="user.isadmin">Admin</div>
            <div class="user-profile__admin-badge" v-if="!user.isadmin">Not Admin</div>
            <div class="user-profile__follower-count">
                <strong>Followers:</strong>{{followers}}
            </div>
            <button @click="chgstate()">Do Admin</button>
        </div>
        <div class="user-profile__twoots-wrapper">
            <TwootItem
                v-for="twoot in user.twoots"
                v-bind:key="twoot.id"
                v-bind:username= "user.username"
                v-bind:twoot= "twoot"
                @favid="printFAV"
                @rtid="printRT"
            />

        </div>
    </div>    
</template>

<script>
import TwootItem from "./TwootItem";

export default {
    name: "UserProfile",
    components: {TwootItem},
    data(){
        return {
            followers : 0,
            user : {
                username : "mamatias",
                firstname : "matias",
                lastname : "torres",
                email : "mamatias@mailinator.com",
                isadmin : true,
                twoots : [
                    {id:1, content:'This is the first twoot of this acount...'},
                    {id:2, content:'Second twoot just for testing...'}
                ]
            }
        }
    },
    watch: {
        // Chequea el dato "followers"
        followers(newVal, oldVal){
            if(newVal > oldVal){
                console.log(`User ${this.user.username} gain 1 follower...`);
            }
        }

    },
    computed: {

    },
    methods:{
        followUser(){
            this.followers = this.followers + 1;
        },
        chgstate(){
            if(this.user.isadmin){
                this.user.isadmin = false;
            }
            else{
                this.user.isadmin = true;
            }
        },
        printFAV(obj){
            console.log(`Twoot # ${obj.id} from user: ${obj.usr} had been FAV...`);
        },
        printRT(obj){
            console.log(`Twoot # ${obj.id} from user: ${obj.usr} had been RT...`);
        }
    },
    mounted(){
        this.followUser();        
    }
    
}
</script>

<style>
    .user-profile {
        display: grid;
        grid-template-columns: 1fr 3fr;
        width: auto;
        padding: 50px 5%;
    }

    .user-profile__user-panel {
        display: flex;
        flex-direction: column;
        margin-right: 50px;
        padding: 20px;
        background-color: white;
        border-radius: 5px;
        border: 1px solid rgb(196, 196, 196);
    }

    .user-profile__admin-badge {
        border-radius: 5px;
        background: rgb(146, 39, 233);
        color: white;
        margin-right: auto;
        padding: 0.2rem 10px 0px 10px;
        font-weight: bold;
    }

    .user-profile__twoots-wrapper {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
    }
</style>