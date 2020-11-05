<template>
    <div>
        <table>
            <tr>
                <td>编号</td>
                <td>名字</td>
                <td>密码</td>
            </tr>
            <tr v-for="user in users">
                <td>{{user.id}}</td>
                <td>{{user.name}}</td>
                <td>{{user.password}}</td>
            </tr>
        </table>
    </div>
</template>

<script>
    export default {
        name: "user",
        data(){
            return {
                users:[
                    {
                        id: 1,
                        name: '三体',
                        password: '刘慈欣'
                    },
                    {
                        id: 2,
                        name: 'java从零到入土',
                        password: '我'
                    }
                ]
            }
        },
        created() {
            var that=this;
            axios.get('http://localhost:8081/getAllUser').then(function (resp) {
                that.users=resp.data;
        })
        }

    }
</script>

<style scoped>

</style>
