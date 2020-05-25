<template>
    <div class="py-0" :class="{'fill-height': fh}">
        <v-container fluid class="fill-height py-0">
            <v-row class="adder-box">
                <v-col cols="12" class="py-0">
                    <v-row align="center" justify="center" class="adder-box-inner">
                        <v-btn color="pink" fab dark @click.stop="adderList = !adderList">
                            <v-icon dark>mdi-shape-square-plus</v-icon>
                        </v-btn>
                    </v-row>
                </v-col>
            </v-row>
        </v-container>
        <v-navigation-drawer v-model="adderList" fixed temporary>
            <v-list>
                <v-list-item v-for="item in availableBlocks" :key="item.title" link @click="addBlock(item)">
                    <v-list-item-icon>
                        <v-icon>{{ item.icon }}</v-icon>
                    </v-list-item-icon>

                    <v-list-item-content>
                        <v-list-item-title>{{ item.title }}</v-list-item-title>
                    </v-list-item-content>
                </v-list-item>
            </v-list>
        </v-navigation-drawer>
    </div>
</template>

<script>
    export default {
        name: "AdderBox",
        props: ['fh'],
        data () {
            return {
                adderList: false,
                availableBlocks: [
                    {
                        title: 'Full-height Header',
                        icon: 'mdi-image-area',
                        type: 'fhh',
                        options: {
                            bgImage: 'img1.jpg',
                            header: 'Big Header Example',
                            description: 'First block is the biggest one'
                        }
                    },
                    {
                        title: 'Three column articles',
                        icon: 'mdi-view-column',
                        type: 'col3',
                        options: {
                            icon1: 'alert-decagram',
                            header1: 'First column',
                            description1: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Mollis nunc sed id semper risus in hendrerit gravida rutrum. Ante in nibh mauris cursus mattis molestie a iaculis at. Id semper risus in hendrerit. Tincidunt augue interdum velit euismod in pellentesque massa. Nam aliquam sem et tortor consequat.',
                            icon2: 'alarm',
                            header2: 'First column',
                            description2: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Mollis nunc sed id semper risus in hendrerit gravida rutrum. Ante in nibh mauris cursus mattis molestie a iaculis at. Id semper risus in hendrerit. Tincidunt augue interdum velit euismod in pellentesque massa. Nam aliquam sem et tortor consequat.',
                            icon3: 'asterisk',
                            header3: 'First column',
                            description3: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Mollis nunc sed id semper risus in hendrerit gravida rutrum. Ante in nibh mauris cursus mattis molestie a iaculis at. Id semper risus in hendrerit. Tincidunt augue interdum velit euismod in pellentesque massa. Nam aliquam sem et tortor consequat.',
                        }
                    },
                ],
            }
        },
        methods: {
            addBlock(block) {
                this.$emit('add-block', block);
                this.adderList = false;
            }
        }

    }
</script>

<style scoped lang="scss">
    .adder-box {
        height: 100%;
        min-height: 200px;
        padding: 20px;
        .adder-box-inner {
            height: 100%;
            background-color: #eeeeee;
            border: 4px dashed #dddddd;
            &:hover {
                background-color: #e5e5e5;
            }
        }
    }
</style>