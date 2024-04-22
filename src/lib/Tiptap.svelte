<script>
    import { onMount, onDestroy } from 'svelte'
    import { Editor } from '@tiptap/core'
    import StarterKit from '@tiptap/starter-kit'
  
    let element
    let editor
  
    onMount(() => {
      editor = new Editor({
        element: element,
        extensions: [
          StarterKit,
        ],
        content: '<h1>Título 1</h1> <h2>Título 2 </h2> <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Pariatur, ipsa. Consequuntur molestiae omnis at accusamus, est provident perferendis debitis quod adipisci unde voluptate ipsam ab tenetur minima voluptas eveniet vel?</p>',
        onTransaction: () => {
          // force re-render so `editor.isActive` works as expected
          editor = editor
        },
      })
      
    })
  
    onDestroy(() => {
      if (editor) {
        editor.destroy()
      }
    })

  </script>
  
  <div class="editor">
    <div class="editor-options">

    {#if editor}
      <button
        on:click={() => editor.chain().focus().toggleHeading({ level: 1}).run()}
        class:active={editor.isActive('heading', { level: 1 })}
      >
        H1
      </button>
      <button
        on:click={() => editor.chain().focus().toggleHeading({ level: 2 }).run()}
        class:active={editor.isActive('heading', { level: 2 })}
      >
        H2
      </button>
      <button on:click={() => editor.chain().focus().setParagraph().run()} class:active={editor.isActive('paragraph')}>
        P
      </button>
    {/if}
    </div>

    <div bind:this={element} />
  </div>
  
  
  <style>
    button.active {
      background: black;
      color: white;
    }
    .editor {
      display: block;
      position: relative;

    }
    .editor-options {
      display: flex;
      justify-content: left;
      gap: 1rem;
    }

  </style>