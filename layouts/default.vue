<template>
  <div class="global-layout">
    <div class="global-layout-header">
      Header
      <a href="/tasks">Tasks</a>
    </div>
    <div class="global-layout-content"><slot /></div>
    <div class="global-layout-footer">
      Footer
    </div>
  </div>
</template>

<style>
  .global-layout {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
  }
  .global-layout-header {
    background: black;
    height: 50px;
    color: white;
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 0px 20px;
  }
  .global-layout-content {
    flex: 1;
  }
  .global-layout-footer {
    background: black;
    color: white;
    display: flex;
    align-items: center;
    gap: 10px;
    height: 50px;
    padding: 0px 20px;
  }
</style>