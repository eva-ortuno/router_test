<template>
    <div class="item">
    <h1 align="center">{{ url }}</h1>
    </div>
</template>
<script>
export default({
    computed: {
        url () {
            const url = window.location.href
            const tool = url.slice(url.lastIndexOf('/')+1)
            let menu = tool.slice(tool.lastIndexOf('-')+1)
            let submenu = tool.slice(0, tool.lastIndexOf('-'))
            if (menu !== 'analytics') {
                menu = tool.slice(tool.indexOf('-')+1)
                menu = menu.split('-').join(' ')
                submenu = tool.slice(0, tool.indexOf('-'))
            }
            if (submenu.includes('-')) {
                submenu = submenu.split('-').join(' ')
            }            
            return this.makeUpperCase(menu) + ' / ' + this.makeUpperCase(submenu)
        }
    },
    methods: {
        makeUpperCase(string) {
            return string.charAt(0).toUpperCase() + string.slice(1)
        }
    }
})
</script>
