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
    <div class="things-card">
        <el-card shadow="hover">
            <div class="things-card-content">
                <div
                    class="things-card__header"
                    :class="{
                        'header-enable': data.enable,
                        'header-disable': !data.enable,
                    }"
                >
                    <div class="things-card-header-icon">
                        <img :src="icon" :alt="data.name" />
                    </div>
                    <div class="things-card-header-name nowrap-name" @click="copyId(data.id, '位号ID')">
                        {{ data.name }}
                    </div>
                    <div title="状态" class="things-card-header-status"></div>
                </div>
                <div class="things-card__body">
                    <div class="things-card-body-content">
                        <ul class="things-body-content-item-column-2">
                            <li class="nowrap-item">
                                <span
                                    ><el-icon><List /></el-icon> 所属模板: </span
                                >{{ profile.name }}
                            </li>
                            <li class="nowrap-item">
                                <span
                                    ><el-icon><Location /></el-icon> 累计标识: </span
                                >{{ data.accrue ? '累计' : '不累计' }}
                            </li>
                            <li class="nowrap-item">
                                <span
                                    ><el-icon><Location /></el-icon> 基值: </span
                                >{{ data.base }}
                            </li>
                            <li class="nowrap-item">
                                <span
                                    ><el-icon><Location /></el-icon> 格式: </span
                                >{{ data.format }}
                            </li>
                            <li class="nowrap-item">
                                <span
                                    ><el-icon><Bottom /></el-icon> 最小值: </span
                                >{{ data.minimum }}
                            </li>
                            <li class="nowrap-item">
                                <span
                                    ><el-icon><Edit /></el-icon> 修改日期: </span
                                >{{ timestamp(data.updateTime) }}
                            </li>
                        </ul>
                        <ul class="things-body-content-item-column-2">
                            <li class="nowrap-item">
                                <span
                                    ><el-icon><Location /></el-icon> 数据类型: </span
                                >{{ type }}
                            </li>
                            <li class="nowrap-item">
                                <span
                                    ><el-icon><Location /></el-icon> 读写类型: </span
                                >{{ rw }}
                            </li>
                            <li class="nowrap-item">
                                <span
                                    ><el-icon><Location /></el-icon> 倍数: </span
                                >{{ data.multiple }}
                            </li>
                            <li class="nowrap-item">
                                <span
                                    ><el-icon><Location /></el-icon> 单位: </span
                                >{{ data.unit }}
                            </li>
                            <li class="nowrap-item">
                                <span
                                    ><el-icon><Top /></el-icon> 最大值: </span
                                >{{ data.maximum }}
                            </li>
                            <li class="nowrap-item">
                                <span
                                    ><el-icon><Sunset /></el-icon> 创建日期: </span
                                >{{ timestamp(data.createTime) }}
                            </li>
                        </ul>
                    </div>
                    <div title="位号描述信息" class="things-card-body-content">
                        <p class="nowrap-description">
                            {{ data.description ? data.description : '无描述信息' }}
                        </p>
                    </div>
                </div>
                <div v-if="!embedded" class="things-card__footer">
                    <div class="things-card-footer-operation">
                        <el-popconfirm
                            title="是否确定停用该位号？"
                            placement="top"
                            :icon="SwitchButton"
                            icon-color="#e6a23c"
                            @confirm="disableThing"
                        >
                            <template #reference>
                                <el-button type="primary" :disabled="!data.enable" link>停用</el-button>
                            </template>
                        </el-popconfirm>
                        <el-popconfirm
                            title="是否确定启用该位号？"
                            placement="top"
                            :icon="CircleCheck"
                            icon-color="#67c23a"
                            @confirm="enableThing"
                        >
                            <template #reference>
                                <el-button type="primary" :disabled="data.enable" link>启用</el-button>
                            </template>
                        </el-popconfirm>
                        <el-popconfirm
                            title="是否确定删除该位号？该位号下的配置将会被全部删除，且该操作不可恢复！"
                            placement="top"
                            :icon="CircleClose"
                            icon-color="#f56c6c"
                            @confirm="deleteThing"
                        >
                            <template #reference>
                                <el-button type="primary" link>删除</el-button>
                            </template>
                        </el-popconfirm>
                        <el-button type="primary" link @click="edit">编辑</el-button>
                        <el-button type="primary" link disabled @click="detail">详情</el-button>
                    </div>
                </div>
            </div>
        </el-card>
    </div>
</template>

<script src="./index.ts" lang="ts" />

<style lang="less">
@import '~@/components/card/styles/things-card.less';
</style>
