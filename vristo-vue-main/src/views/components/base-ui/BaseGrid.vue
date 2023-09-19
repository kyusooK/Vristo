<template>
</template>

<script>
import BaseEntity from './BaseEntity.vue';
import BaseSecurity from './BaseSecurity.vue';

export default {
    name: 'BaseGrid',
    data: () => ({
        flex: null,
        tick : true,
        openDialog : false,
        itemToEdit: null,
        selectedRow: null,
        path: 'path',
        repository: null,
    }),
    mixins:[
        BaseEntity,
        BaseSecurity
    ],
    // computed: {
    //     username(){
    //         return this.getUserName();
    //     }
    // },
    async created(){
        
        this.newValue = {name: 'test'}
        var me = this;
        var list = await me.search();
        this.$emit('update:modelValue', list);
        // this.dataService = new DataService();
        // this.exportService = new ExportService();
    }, 
    // beforeDestroy() {
    //     this.exportService.cancelExcelExport();
    // },
    methods:{
        // flexInitialized(flexGrid) {
        //     this.flex = flexGrid;
        //     this.$refs.flexGrid = flexGrid;
        //     let sd = new wjcCore.SortDescription("country", true);
        //     flexGrid.collectionView.sortDescriptions.push(sd);
        // },
        // onSelectionChanged(s) {
        //     if (s && s.collectionView) {
        //         let selectedItem = s.collectionView.currentItem;
        //         if (selectedItem) {
        //             this.selectedRow = selectedItem;
        //         }
        //     }
        // },
        addNewRow() {
            this.newValue = null
            this.openDialog = true;
        },
        // editSelectedRow() {
        //     const flexGrid = this.$refs.flexGrid;
        //     const view = flexGrid.collectionView;

        //     if (view.currentItem) {
        //         this.itemToEdit = JSON.parse(JSON.stringify(view.currentItem));
        //         this.newValue = this.itemToEdit
        //         this.edit(this.itemToEdit);
        //         this.$set(this, 'selectedRow', this.itemToEdit);

        //         this.$nextTick(() => {
        //             this.openDialog = true;
        //         });
        //     }
        // },
        // flexDetailsInitialized(flexGridDetails) {
        //     this.$refs.flexGridDetails = flexGridDetails;
        // },
        // getSelectedItem(){
        //     const flexGrid = this.$refs.flexGrid;
        //     const view = flexGrid.collectionView;
        //     return view.currentItem

        // },
        // async deleteSelectedRows() {
        //     try {
        //         if (!this.offline) {
        //             const flexGrid = this.$refs.flexGrid;
        //             const view = flexGrid.collectionView;
        //             const selectedIndex = view.currentPosition;
                    
        //             if (view.currentItem) {
        //                 await this.repository.delete(view.currentItem)
                        
        //                 view.remove(view.currentItem);

        //                 this.value = view.sourceCollection;
        //                 if (this.value.length > 0) {
        //                     if (selectedIndex > 0) {
        //                         this.selectedRow = this.value[Math.min(selectedIndex, this.value.length - 1)];
        //                     } else {
        //                         this.selectedRow = this.value[0];
        //                     }
        //                 } else {
        //                     this.selectedRow = null;
        //                 }
        //             }
        //         }
        //     } catch(e) {
        //         this.$EventBus.$emit('show-error', e);
        //     }
        // },
        // groupPanelInitialized: function (ctl) {
        //     this.groupPanel = ctl;
        //     if (this.flex) {
        //         this.groupPanel.grid = this.flex;
        //     }
        // },
        // exportToPdf: function() {
        //     this.exportService.exportToPdf(this.flex, {
        //         countryMap: this._countryMap,
        //         colorMap: this._colorMap,
        //         historyCellTemplate: this.historyCellTemplate
        //     });
        // },
        // _buildDataMap: function (items) {
        //     const map = [];
        //     for (let i = 0; i < items.length; i++) {
        //         map.push({ key: i, value: items[i] });
        //     }
        //     return new DataMap(map, 'key', 'value');
        // },
        // getFlex: function () {
        //     return this.flex;
        // },
        // departmentId(href){
        //     if(href){
        //         return href.split('/')[2]
        //     }
        //     return null;
        // },
        // getChangeCls: function (value) {
        //     if (wjCore.isNumber(value)) {
        //         if (value > 0) {
        //             return 'change-up';
        //         }
        //         if (value < 0) {
        //             return 'change-down';
        //         }
        //     }
        //     return '';
        // },
        append() {
            this.tick = false;
            this.openDialog = false
            
            if (!this.value) {
                this.value = [];
            }
            const newItem = { ...this.newValue};

            this.value.push(newItem);
            this.$emit('input', this.value);

            this.$nextTick(() => {
                this.tick = true;
            });
        },
        remove(value){
            var where = -1;
            for(var i=0; i<this.value.length; i++){
                if(this.value[i]._links.self.href == value._links.self.href){
                    where = i;
                    break;
                }
            }
            if(where > -1){
                this.value.splice(i, 1);
                this.$emit('input', this.value);
            }
        },


        async search(query) {
            var me = this;
            if(me.offline){
                if(!me.modelValue) me.modelValue = [];
                return;
            } 
            var temp = null;

            if(!me.offline){
                temp = await this.repository.find(query)
            }

            return temp;
        },
        edit(){
            for(var i = 0; i < this.value.length; i++){
                if(this.value[i].index == this.itemToEdit.index){
                    this.value[i] = this.itemToEdit
                    break;
                }
            }
            this.openDialog = false;
        }
    },
    // filters: {
    //     safeCurrency: function (value) {
    //         if (wjCore.isNumber(value)) {
    //             return wjCore.Globalize.formatNumber(value, 'c');
    //         }
    //         if (!wjCore.isUndefined(value) && value !== null) {
    //             return wjCore.changeType(value, wjCore.DataType.String);
    //         }
    //         return '';
    //     }
    // },
}
</script>

<style>
</style>

