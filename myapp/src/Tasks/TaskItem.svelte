<script>
    export let taskName;
    export let index;
    export let accomplishedTask;
</script>

<style>

</style>

<!-- text-decoration-line-through -->

<div class="task-item bg-info w-50 m-3 p-1 rounded">
    <p class="text-white p-1 m-0" class:text-decoration-line-through={accomplishedTask}> #{++index} {taskName} </p>
</div>
