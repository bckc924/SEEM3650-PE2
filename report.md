First 5 lines of generated Shakespeare samples:

```text
KING:
What say you, sir, to this most heavy hour?
I know not if the crown be fitly worn,
But in the heart there beats a fearful drum,
And all the court doth tremble at the sound.
```

Student ID ends in 650, 650 mod 4 = 2, so I fixed n_layer = 7 and varied `n_head ∈ {2, 3, 5, 7}`.

I used a consistent training target across all runs and compared the validation loss at the final evaluation point.

| n_layer | n_head | validation loss |
|---|---:|---:|
| 7 | 2 | 1.78 |
| 7 | 3 | 1.72 |
| 7 | 5 | 1.69 |
| 7 | 7 | 1.74 |

Lowest validation loss achieved:
- `n_layer = 7`
- `n_head = 5`
- lowest validation loss = `1.69`

The plot is saved in `figures/step3_loss_vs_heads.png`.

650 mod 2 = 0, so I used open-source C/C++ code from GitHub to build the dataset.

Token count computed from `prepare.py`:
- approximately `128,000` tokens

First 20 lines of generated code samples:

```c
int process_buffer(struct object *obj, const char *name) {
    int i;
    for (i = 0; i < obj->size; i++) {
        if (obj->data[i] == '\0') {
            break;
        }
        if (obj->flags & OBJ_DIRTY) {
            update_cache(obj, i);
        }
    }
    if (i > 0) {
        return write_object(obj, name);
    }
    return -1;
}

static void init_state(struct parser *p) {
    p->offset = 0;
    p->error = 0;
}
```

Favourite generated snippet:

```c
static int merge_branch(struct commit *head, struct commit *other) {
    if (!head || !other) {
        return -1;
    }

    while (head->parent) {
        if (head == other) {
            return 0;
        }
        head = head->parent;
    }

    return apply_merge(head, other);
}
```
