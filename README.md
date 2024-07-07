# landlord-registration-page

請依據這個vue檔幫我建立註冊的頁面:
<!-- 房東註冊頁面(只有房東需要註冊) -->
<script>
import dataStore from "@/stores/dataStore";
import { mapState, mapActions } from "pinia";
export default {
    data(){
        return {
            owner_account:"",
            owner_pwd:"",
            owner_identity:"",
            owner_name:"",
            owner_email:"",
            owner_phone:"",
            registerList:[],//存放註冊資訊
        }
    },
    computed: {
        ...mapState(dataStore, ['page','registerObj'])
    },
    methods: {
        ...mapActions(dataStore,['setPage','setRegisterObj']),
        
        register(){
            let registerObj1 = {
                owner_account: this.owner_account,
                owner_pwd: this.owner_pwd,
                owner_email: this.owner_email,
                owner_phone: this.owner_phone,
                owner_identity: this.owner_identity,
                owner_name: this.owner_name
            };
            console.log('Sending data:', registerObj1); // 印出來看有沒有吃到輸入資料
            // url
            fetch("http://localhost:8080/rent/account", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                },
                body: JSON.stringify(registerObj1),
            })
            .then(res => {
                if (!res.ok) {
                    throw new Error('Network response was not ok');
                }
                return res.json();
            })
            .then(data => {
                console.log(data);
                this.setRegisterObj(data);
                console.log('pinia裡的', this.registerObj);
            })
            .catch(error => {
                console.error('fetch有問題:', error);
            });
        }

    },
    mounted(){
    
    }
}
</script>

<template>
<div class="inputdiv">
    <p>帳號:<input type="text" v-model="owner_account"></p>
    <p>密碼:<input type="password" v-model="owner_pwd"></p>
    <p>真實姓名:<input type="text" v-model="owner_name"></p>
    <p>身分證字號:<input type="text" v-model="owner_identity"></p>
    <p>手機號:<input type="text" v-model="owner_phone"></p>
    <p>電子郵件:<input type="email" v-model="owner_email"></p>
    <button type="submit" @click="register()">確認</button>
</div>
</template>

<style scoped lang="scss">
*{margin-left: 10%;}
</style>

## Collaborate with GPT Engineer

This is a [gptengineer.app](https://gptengineer.app)-synced repository 🌟🤖

Changes made via gptengineer.app will be committed to this repo.

If you clone this repo and push changes, you will have them reflected in the GPT Engineer UI.

## Tech stack

This project is built with .

- Vite
- React
- shadcn-ui
- Tailwind CSS

## Setup

```sh
git clone https://github.com/GPT-Engineer-App/landlord-registration-page.git
cd landlord-registration-page
npm i
```

```sh
npm run dev
```

This will run a dev server with auto reloading and an instant preview.

## Requirements

- Node.js & npm - [install with nvm](https://github.com/nvm-sh/nvm#installing-and-updating)
