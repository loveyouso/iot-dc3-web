<!--
  - Copyright 2022 Pnoker All Rights Reserved
  -
  - Licensed under the Apache License, Version 2.0 (the "License");
  - you may not use this file except in compliance with the License.
  - You may obtain a copy of the License at
  -
  -      https://www.apache.org/licenses/LICENSE-2.0
  -
  - Unless required by applicable law or agreed to in writing, software
  - distributed under the License is distributed on an "AS IS" BASIS,
  - WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  - See the License for the specific language governing permissions and
  - limitations under the License.
  -->

<template>
    <div class="tool-card">
        <el-card :shadow="embedded == '' ? 'hover' : 'never'">
            <el-form
                ref="formDataRef"
                class="tool-card-body"
                :model="reactiveData.formData"
                :rules="formRule"
                :inline="true"
            >
                <div class="tool-card-body-form">
                    <el-form-item v-if="embedded == ''" prop="deviceId" label="设备">
                        <el-select
                            v-model="reactiveData.formData.deviceId"
                            class="edit-form-special"
                            placeholder="请选择设备"
                            clearable
                            @change="pointDictionaryChange"
                            @visible-change="deviceDictionaryVisible"
                        >
                            <div class="tool-select">
                                <el-form-item class="tool-select-input">
                                    <el-input
                                        v-model="reactiveData.deviceQuery"
                                        placeholder="请输入设备名称"
                                        clearable
                                        @input="deviceDictionary"
                                    />
                                </el-form-item>
                                <el-pagination
                                    class="tool-select-pagination"
                                    :hide-on-single-page="true"
                                    layout="prev, pager, next"
                                    :pager-count="5"
                                    :page-size="+reactiveData.devicePage.size"
                                    :current-page="+reactiveData.devicePage.current"
                                    :total="+reactiveData.devicePage.total"
                                    small
                                    background
                                    @current-change="deviceCurrentChange"
                                ></el-pagination>
                            </div>
                            <el-option
                                v-for="dictionary in reactiveData.deviceDictionary"
                                :key="dictionary.value"
                                :label="dictionary.label"
                                :value="dictionary.value"
                            ></el-option>
                        </el-select>
                    </el-form-item>
                    <el-form-item v-if="embedded == ''" prop="pointId" label="位号">
                        <el-select
                            v-model="reactiveData.formData.pointId"
                            class="edit-form-special"
                            placeholder="请选择位号"
                            clearable
                            @visible-change="pointDictionaryVisible"
                        >
                            <div class="tool-select">
                                <el-form-item class="tool-select-input">
                                    <el-input
                                        v-model="reactiveData.pointQuery"
                                        placeholder="请输入位号名称"
                                        clearable
                                        @input="pointDictionary"
                                    />
                                </el-form-item>
                                <el-pagination
                                    class="tool-select-pagination"
                                    :hide-on-single-page="true"
                                    layout="prev, pager, next"
                                    :pager-count="5"
                                    :page-size="+reactiveData.pointPage.size"
                                    :current-page="+reactiveData.pointPage.current"
                                    :total="+reactiveData.pointPage.total"
                                    small
                                    background
                                    @current-change="pointCurrentChange"
                                ></el-pagination>
                            </div>
                            <el-option
                                v-for="dictionary in reactiveData.pointDictionary"
                                :key="dictionary.value"
                                :label="dictionary.label"
                                :value="dictionary.value"
                            ></el-option>
                        </el-select>
                    </el-form-item>
                    <el-form-item v-if="embedded == 'device'" prop="name" label="位号名称">
                        <el-input
                            v-model="reactiveData.formData.name"
                            class="edit-form-default"
                            placeholder="请输入位号名称"
                            clearable
                            @keyup.enter="search"
                        >
                        </el-input>
                    </el-form-item>
                    <el-form-item v-if="embedded == 'device'" prop="enable" label="使能">
                        <el-select
                            v-model="reactiveData.formData.enable"
                            class="edit-form-small"
                            placeholder="请选择使能"
                            clearable
                        >
                            <el-option label="启用" :value="true"></el-option>
                            <el-option label="停用" :value="false"></el-option>
                        </el-select>
                    </el-form-item>
                </div>
                <el-form-item class="tool-card-body-button">
                    <el-button type="primary" :icon="Search" @click="search">搜索</el-button>
                    <el-button :icon="RefreshRight" @click="reset">重置</el-button>
                </el-form-item>
            </el-form>
            <div class="tool-card-footer">
                <div class="tool-card-footer-button">
                    <el-button v-if="embedded == ''" type="success" :icon="Plus" disabled>新增</el-button>
                </div>
                <div class="tool-card-footer-page">
                    <el-pagination
                        layout="total, prev, pager, next, sizes"
                        :page-sizes="[6, 12, 24, 36, 48]"
                        :page-size="+page.size"
                        :current-page="+page.current"
                        :total="+page.total"
                        background
                        @size-change="sizeChange"
                        @current-change="currentChange"
                    >
                    </el-pagination>
                    <el-tooltip class="item" effect="dark" content="刷新" placement="top">
                        <el-button :icon="Refresh" circle @click="refresh"></el-button>
                    </el-tooltip>
                </div>
            </div>
        </el-card>
    </div>
</template>

<script src="./index.ts" lang="ts" />

<style lang="less">
@import '~@/components/card/styles/tool-card.less';
</style>
