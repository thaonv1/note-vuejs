<template>
    <div class="user-dashboard">
        <div class="list-user-comp">
            <h4>List User</h4>
            <!-- Listen event 'userSelected' emitted from child and process it using 'childrenSelectUser' -->
            <ListUser @userSelected="childrenSelectUser"></ListUser>
        </div>
        <hr>
        <div class="user-detail-comp">
            <h4>User Detail</h4>
            <!-- pass 'userSelectedFromChild', child will use props 'userDetailInfo' -->
            <UserDetail :userDetailInfo="userSelectedFromChild"></UserDetail>
        </div>
    </div>
</template>

<script>
    import ListUser from './ListUser.vue'
    import UserDetail from './UserDetail.vue'
    export default {
        components: {
            ListUser,
            UserDetail
        },
        data() {
            return {
                userSelectedFromChild: {}
            }
        },
        methods: {
            // Process event emitted from child
            childrenSelectUser(user) {
                console.log(user)
                this.userSelectedFromChild = user
            }
        }
    }
</script>

<style lang="scss" scoped>
</style>