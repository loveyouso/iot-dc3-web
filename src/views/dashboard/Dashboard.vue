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
    <iframe
        class="things-dashboard-iframe"
        frameborder="no"
        border="0"
        marginwidth="0"
        marginheight="0"
        :src="iframeUrl"
    ></iframe>
</template>

<script src="./index.ts" lang="ts" />

<style lang="less">
.things-dashboard-iframe {
    width: 100%;
    height: 100%;
}
</style>
