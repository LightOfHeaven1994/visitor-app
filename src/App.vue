<template>
    <div id="app" class="small-container">
        <h1>Visitors</h1>
        <visitor-form @add:visitor="addVisitor"/>
        <visitor-table
                :visitors="visitors"
                @delete:visitor="deleteVisitor"
                @edit:visitor="editVisitor"
        />
    </div>
</template>

<script>
    import VisitorTable from '@/components/VisitorTable.vue'
    import VisitorForm from "./components/VisitorForm";

    export default {
        name: 'app',
        components: {
            VisitorForm,
            VisitorTable,
        },
        data() {
            return {
                visitors: []
            }
        },
        methods: {
            addVisitor(visitor) {
                let lastId = this.visitors.length > 0 ?
                    this.visitors[this.visitors.length - 1].id :
                    0;
                let id = lastId + 1;
                let newVisitor = {...visitor, id}
                this.visitors = [...this.visitors, newVisitor]
            },
            deleteVisitor(id) {
                this.visitors = this.visitors.filter(
                    visitor => visitor.id !== id
                )
            },
            editVisitor(id, updatedVisitor) {
                this.visitors = this.visitors.map(visitor =>
                    visitor.id === id ? updatedVisitor : visitor
                )
            }
        }
    }
</script>

<style>
    button {
        background: #009435;
        border: 1px solid #009435;
    }

    .small-container {
        max-width: 680px;
    }
</style>