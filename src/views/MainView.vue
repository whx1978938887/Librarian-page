<template>
    <div class="layout">
        <Layout>
            <Header>
                <Menu mode="horizontal" theme="dark" active-name="1">
                    <div class="layout-logo"></div>
                    <div class="layout-nav">
                        <MenuItem name="1">
                        <Icon type="ios-navigate"></Icon>
                        Item 1
                        </MenuItem>
                        <MenuItem name="2">
                        <Icon type="ios-keypad"></Icon>
                        Item 2
                        </MenuItem>
                        <MenuItem name="3">
                        <Icon type="ios-analytics"></Icon>
                        Item 3
                        </MenuItem>
                        <MenuItem name="4">
                        <Icon type="ios-paper"></Icon>
                        Item 4
                        </MenuItem>
                    </div>
                </Menu>
            </Header>
            <Layout>
                <Sider hide-trigger :style="{ background: '#fff' }">
                    <Menu theme="light" width="auto" @on-select="onselect">
                        <MenuItem :name="item.component" v-for="item in components" :key="item">
                        <Icon :type="item.icon"></Icon>
                        {{ item.name }}
                        </MenuItem>
                    </Menu>
                </Sider>
                <Layout :style="{ padding: '0 24px 24px' }">
                    <Breadcrumb :style="{ margin: '24px 0' }">
                        <BreadcrumbItem>Home</BreadcrumbItem>
                        <BreadcrumbItem>Components</BreadcrumbItem>
                        <BreadcrumbItem>Layout</BreadcrumbItem>
                    </Breadcrumb>
                    <Content :style="{ padding: '24px', minHeight: '500px', background: '#fff' }">
                        <RouterView />
                    </Content>
                </Layout>
            </Layout>
        </Layout>
    </div>
</template>
<script>
import { Icon, MenuItem } from 'view-ui-plus';

export default {
    data() {
        return {
            components: []
        }
    },
    mounted() {
        this.$router.push('/main/home')
        this.$axios.get('/user/permissions', {
        }).then((successResponse) => {
            this.components = successResponse.data.object
        }).catch((failResponse) => {
            this.$Message.info(failResponse)
        })
    },
    components: {
        Icon,
        MenuItem
    },
    methods: {
        onselect(name) {
            this.$router.push('/main/' + name)
        }
    }
}
</script>
<style>
.layout {
    border: 1px solid #d7dde4;
    background: #f5f7f9;
    position: relative;
    border-radius: 4px;
    overflow: hidden;
}

.layout-logo {
    width: 100px;
    height: 30px;
    background: #5b6270;
    border-radius: 3px;
    float: left;
    position: relative;
    top: 15px;
    left: 20px;
}

.layout-nav {
    width: 420px;
    margin: 0 auto;
    margin-right: 20px;
}
</style>
