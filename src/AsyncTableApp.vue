<template>
    <div
        id="app"
    >
        <vue-ads-table
            :columns="columns"
            :rows="rows"
            :filter="filter"
            :start="start"
            :end="end"
            @filter-change="filterChanged"
            :call-rows="callRows"
            :call-children="callChildren"
            :call-temp-rows="callTempRows"
        >
            <!--&lt;!&ndash; Will be applied on the name column for the rows with an _id of tiger &ndash;&gt;-->
            <!--<template slot="name_tiger" slot-scope="props">test cell - {{ props.row[props.column.property] }}</template>-->
            <!--&lt;!&ndash; Will be applied on the city column &ndash;&gt;-->
            <!--<template slot="city" slot-scope="props">test column - {{ props.row.city }}</template>-->
            <!--&lt;!&ndash; Will be applied on the row with _id tiger &ndash;&gt;-->
            <!--<template slot="_tiger" slot-scope="props">test row - {{ props.row[props.column.property] }}</template>-->
            <!--<template slot="no-rows">Geen resultaten</template>-->
            <!--<template slot="sort-icon" slot-scope="props">{{ props.direction === null ? 'null' : (props.direction ? 'up' : 'down') }}</template>-->
            <!--<template slot="toggle-children-icon" slot-scope="props">{{ props.expanded ? 'open' : 'closed' }}</template>-->
        </vue-ads-table>
    </div>
</template>

<script>
import './assets/css/tailwind.css';
import '../node_modules/@fortawesome/fontawesome-free/css/all.css';

import VueAdsTable from './components/Table';

export default {
    name: 'AsyncTableApp',

    components: {
        VueAdsTable,
    },

    data () {
        let rows = [
            {
                _id: 'tiger',
                name: 'Tiger Nixon',
                function: 'System Architect',
                city: 'Edinburgh',
                id: '5421',
                since: '2011/04/25',
                budget: '$320,800',
                _children: [
                    {
                        name: 'Garrett Winters',
                        function: 'Accountant',
                        city: 'Tokyo',
                        id: '8422',
                        since: '2011/07/25',
                        budget: '$170,750',
                    },
                    {
                        name: 'Airi Satou',
                        function: 'Accountant',
                        city: 'Tokyo',
                        id: '5407',
                        since: '2008/11/28',
                        budget: '$162,700',
                        _showChildren: true,
                        _children: [
                            {
                                name: 'Gloria Little',
                                function: 'Systems Administrator',
                                city: 'New York',
                                id: '1721',
                                since: '2009/04/10',
                                budget: '$237,500',
                            },
                            {
                                name: 'Bradley Greer',
                                function: 'Software Engineer',
                                city: 'London',
                                id: '2558',
                                since: '2012/10/13',
                                budget: '$132,000',
                            },
                        ],
                    },
                    {
                        name: 'Ashton Cox',
                        function: 'Junior Technical Author',
                        city: 'San Francisco',
                        id: '1562',
                        since: '2009/01/12',
                        budget: '$86,000',
                    },
                ],
            },
            {
                name: 'Garrett Winters',
                function: 'Accountant',
                city: 'Tokyo',
                id: '8422',
                since: '2011/07/25',
                budget: '$170,750',
                _hasChildren: true,
            },
            {
                name: 'Ashton Cox',
                function: 'Junior Technical Author',
                city: 'San Francisco',
                id: '1562',
                since: '2009/01/12',
                budget: '$86,000',
            },
            {
                name: 'Cedric Kelly',
                function: 'Senior Javascript Developer',
                city: 'Edinburgh',
                id: '6224',
                since: '2012/03/29',
                budget: '$433,060',
            },
            {
                name: 'Airi Satou',
                function: 'Accountant',
                city: 'Tokyo',
                id: '5407',
                since: '2008/11/28',
                budget: '$162,700',
            },
            {
                name: 'Brielle Williamson',
                function: 'Integration Specialist',
                city: 'New York',
                id: '4804',
                since: '2012/12/02',
                budget: '$372,000',
            },
            {
                name: 'Herrod Chandler',
                function: 'Sales Assistant',
                city: 'San Francisco',
                id: '9608',
                since: '2012/08/06',
                budget: '$137,500',
            },
            {
                name: 'Rhona Davidson',
                function: 'Integration Specialist',
                city: 'Tokyo',
                id: '6200',
                since: '2010/10/14',
                budget: '$327,900',
            },
            {
                name: 'Colleen Hurst',
                function: 'Javascript Developer',
                city: 'San Francisco',
                id: '2360',
                since: '2009/09/15',
                budget: '$205,500',
            },
            {
                name: 'Sonya Frost',
                function: 'Software Engineer',
                city: 'Edinburgh',
                id: '1667',
                since: '2008/12/13',
                budget: '$103,600',
            },
        ];
        let columns = [
            {
                property: 'id',
                title: 'ID#',
                direction: null,
                filterable: true,
            },
            {
                property: 'name',
                title: 'Name',
                direction: null,
                filterable: true,
            },
            {
                property: 'function',
                title: 'Function',
                direction: null,
                filterable: true,
            },
            {
                property: 'city',
                title: 'City',
                direction: null,
                filterable: true,
            },
            {
                property: 'since',
                title: 'Since',
                direction: null,
                filterable: true,
            },
            {
                property: 'budget',
                title: 'Budget',
                direction: null,
                filterable: true,
            },
        ];

        rows.length = 20;

        return {
            rows,
            columns,
            filter: '',
            start: 0,
            end: 10,
        };
    },

    methods: {
        sleep (ms) {
            return new Promise(resolve => setTimeout(resolve, ms));
        },

        filterChanged (filter) {
            this.filter = filter;
        },

        async callRows (indexesToLoad) {
            await this.sleep(1000);

            return indexesToLoad.map(index => {
                return {
                    name: 'Herrod Chandler',
                    function: 'Sales Assistant',
                    city: 'San Francisco',
                    id: '9608',
                    since: '2012/08/06',
                    budget: '$137,500',
                };
            });
        },

        async callChildren (parent) {
            await this.sleep(1000);
            return [
                {
                    name: 'Jonas Alexander',
                    function: 'Developer',
                    city: 'San Francisco',
                    id: '8196',
                    since: '2010/07/14',
                    budget: '$86,500',
                },
            ];
        },

        async callTempRows () {
            await this.sleep(1000);

            return {
                rows: [],
                total: 0,
            };
        },
    },
};
</script>
