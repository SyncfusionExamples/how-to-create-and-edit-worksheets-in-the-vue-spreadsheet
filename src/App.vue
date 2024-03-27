<script>
  import { SpreadsheetComponent, SheetsDirective, SheetDirective, RangesDirective, 
      RangeDirective, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-vue-spreadsheet';
  import { ButtonComponent } from '@syncfusion/ej2-vue-buttons';
  import datasource from './default.json';
  export default{
    components: {
      'ejs-spreadsheet': SpreadsheetComponent,
      'e-sheets': SheetsDirective,
      'e-sheet': SheetDirective,
      'e-ranges': RangesDirective,
      'e-range': RangeDirective,
      'e-columns': ColumnsDirective,
      'e-column': ColumnDirective,
      'ejs-button': ButtonComponent
    },
    data(){
      return{
        data: datasource.defaultData,
        customWidth: 130,
      }
    },
    methods: {
      created: function() {
        var spreadsheet = this.$refs.spreadsheet;
        spreadsheet.cellFormat({ fontWeight: 'bold', textAlign: 'center' }, 'A1:F1');
        // inserting a new sheet with data at 1st index
         // You can also insert empty sheets by specifying the start and end sheet index instead of sheet model
        spreadsheet.insertSheet([
          {
            index: 0,
            name: "Order Details",
            ranges: [{ dataSource: this.data }],
            columns: [{ width: 150 }, { width: 110 }, { width: 110 }, { width: 110 }, { width: 85 }, { width: 85 }]
          }
        ]);
      },
      btnClick(){
        var spreadsheet = this.$refs.spreadsheet;
        // Start editing
        spreadsheet.startEdit();
        //End editing
        // spreadsheet.endEdit();
        // Cancel editing
        //spreadsheet.closeEdit();
      },
      onEdit:function(args){
        if(args.address.includes('E')){
          args.cancel = true;
        }
      }
    }
  }
</script>

<template>
  <div>
  <ejs-button style="margin: 5px;" v-on:click="btnClick">Save</ejs-button>
    <ejs-spreadsheet ref="spreadsheet" :created="created" :cellEdit="onEdit">
       
    </ejs-spreadsheet>
  </div>

  <!-- <e-sheets>
        <e-sheet>
          <e-ranges>
            <e-range :dataSource="data"></e-range>
          </e-ranges>
          <e-columns>
            <e-column :width="customWidth"></e-column>
            <e-column :width="customWidth"></e-column>
            <e-column :width="customWidth"></e-column>
            <e-column :width="customWidth"></e-column>
            <e-column :width="customWidth"></e-column>
            <e-column :width="customWidth"></e-column>
          </e-columns>
        </e-sheet> 
        <e-sheet state="Hidden"></e-sheet> 
      </e-sheets> -->
</template>

<style>
  @import "../node_modules/@syncfusion/ej2-base/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-dropdowns/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-inputs/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-navigations/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-popups/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-grids/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-vue-spreadsheet/styles/material.css";
</style>
