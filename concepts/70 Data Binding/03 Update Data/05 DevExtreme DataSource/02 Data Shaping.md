Data shaping is implemented by the [DataSource](/api-reference/30%20Data%20Layer/DataSource '/Documentation/ApiReference/Data_Layer/DataSource/') component and its methods. To call them, use the [getDataSource()](/api-reference/10%20UI%20Components/DataHelperMixin/3%20Methods/getDataSource().md '/Documentation/ApiReference/UI_Components/dxDataGrid/Methods/#getDataSource') method to get a **DataSource** instance from your UI component. Alternatively, you can use a standalone instance saved in a constant/component property when you created the **DataSource**.

[note] The **getDataSource()**.[load()](/api-reference/30%20Data%20Layer/DataSource/3%20Methods/load().md '/Documentation/ApiReference/Data_Layer/DataSource/Methods/#load') method re-renders the component. To avoid this behavior, use **getDataSource()**.[store()](/api-reference/30%20Data%20Layer/DataSource/3%20Methods/store().md '/Documentation/ApiReference/Data_Layer/DataSource/Methods/#store').[load()](/api-reference/30%20Data%20Layer/Store/3%20Methods/load().md '/Documentation/ApiReference/Data_Layer/ArrayStore/Methods/#load') instead.

The following code obtains a **DataSource** instance using both approaches and calls one of the data shaping methods&mdash;[filter(filterExpr)](/api-reference/30%20Data%20Layer/DataSource/3%20Methods/filter(filterExpr).md '/Documentation/ApiReference/Data_Layer/DataSource/Methods/#filterfilterExpr'). Such methods only set up data shaping settings. To apply them, the [load()](/api-reference/30%20Data%20Layer/DataSource/3%20Methods/load().md '/Documentation/ApiReference/Data_Layer/DataSource/Methods/#load') method is called.

---
##### jQuery

    <!-- tab: index.js -->
    $(function() {
        var dataSource = new DevExpress.data.DataSource({
            // ...
            // DataSource is configured here
            // ...
        });

        // ===== or getting a DataSource from the UI component (DataGrid here) =====
        var dataSource = $("#dataGridContainer").dxDataGrid("getDataSource");

        // ===== applying a filter =====
        dataSource.filter(['age', '>', 18]);
        dataSource.load();
    });

##### Angular

- **Using a standalone DataSource instance**

        <!-- tab: app.component.ts -->
        import { Component } from '@angular/core';
        import DataSource from 'devextreme/data/data_source';

        @Component({
            selector: 'app-root',
            templateUrl: './app.component.html',
            styleUrls: ['./app.component.css']
        })
        export class AppComponent {
            dataSource: DataSource;
            constructor() {
                this.dataSource = new DataSource({
                    // ...
                    // DataSource is configured here
                    // ...
                });
            }
            filter() {
                this.dataSource.filter(['age', '>', 18]);
                this.dataSource.load();
            }
        }

- **Getting a DataSource instance from the UI component (DataGrid here)**

        <!-- tab: app.component.ts -->
        import { Component } from '@angular/core';
        import { DxDataGridComponent } from 'devextreme-angular';

        @Component({
            selector: 'app-root',
            templateUrl: './app.component.html',
            styleUrls: ['./app.component.css']
        })
        export class AppComponent {
            @ViewChild(DxDataGridComponent, { static: false }) dataGrid: DxDataGridComponent;
            // Prior to Angular 8
            // @ViewChild(DxDataGridComponent) dataGrid: DxDataGridComponent;
            filter() {
                const dataSource = this.dataGrid.instance.getDataSource();
                dataSource.filter(['age', '>', 18]);
                dataSource.load();
            }
        }

##### Vue

- **Using a standalone DataSource instance**

        <!-- tab: App.vue -->
        <template>
            <!-- ... -->
        </template>
        <script>
        import DataSource from 'devextreme/data/data_source';
        const dataSource = new DataSource({
            // ...
            // DataSource is configured here
            // ...
        });

        export default {
            data() {
                return {
                    dataSource
                }
            },
            methods: {
                filter() {
                    dataSource.filter(['age', '>', 18]);
                    dataSource.load();
                }
            }
        }
        </script>

- **Getting a DataSource instance from the UI component (DataGrid here)**

        <!-- tab: App.vue -->
        <template>
            <DxDataGrid ... 
                ref="myDataGrid">
            </DxDataGrid>
        </template>

        <script>
        import 'devextreme/dist/css/dx.light.css';
        import DxDataGrid from 'devextreme-vue/data-grid';

        export default {
            components: {
                DxDataGrid
            },
            data() {
                return {
                    // ...
                }
            },
            methods: {
                filter() {
                    const dataSource = this.$refs['myDataGrid'].instance.getDataSource();
                    dataSource.filter(['age', '>', 18]);
                    dataSource.load();
                }
            }
        }
        </script>

##### React

- **Using a standalone DataSource instance**

        <!-- tab: App.js -->
        import React from 'react';
        import DataSource from 'devextreme/data/data_source';

        const dataSource = new DataSource({
            // ...
            // DataSource is configured here
            // ...
        });

        class App extends React.Component {
            filter() {
                dataSource.filter(['age', '>', 18]);
                dataSource.load();
            }
            render() {
                return (
                    {/* ... */}
                );
            }
        }
        export default App;

- **Getting a DataSource instance from the UI component (DataGrid here)**

        <!-- tab: App.js -->
        import React from 'react';
        import 'devextreme/dist/css/dx.light.css';
        import DataGrid from 'devextreme-react/data-grid';

        class App extends React.Component {
            constructor(props) {
                super(props);
                this.dataGridRef = React.createRef();
            }
            filter() {
                const dataSource = this.dataGridRef.current.instance().getDataSource();
                dataSource.filter(['age', '>', 18]);
                dataSource.load();
            }
            render() {
                return (
                    <DataGrid ...
                        ref={this.dataGridRef}>
                    </DataGrid>
                );
            }
        }
        export default App;

---