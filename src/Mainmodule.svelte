<script context="module">
    import Mymodule, {updateString} from './sub/Mymodule.svelte';

    let s1 = updateString('Hello');
</script>


<h2>Use function from a sub module</h2>

Output is: {s1}
