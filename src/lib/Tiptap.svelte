<script>
    import { onMount, onDestroy } from 'svelte'
    import { Editor } from '@tiptap/core'
    import StarterKit from '@tiptap/starter-kit'
    import Placeholder from '@tiptap/extension-placeholder'
    let element
    let editor

    onMount(() => {
      editor = new Editor({
        element: element,
        extensions: [
          StarterKit,
          Placeholder.configure({placeholder: 'Escribir por aquí...', emptyEditorClass: 'is-editor-empty'}),
        ],

        content: '',
        // placeholder

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