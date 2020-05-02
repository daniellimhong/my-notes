# What is Git? 

**What is Git?**

- Distributed Version Control System

**How Does Git Store Information**

- At its core, git is like a key value store
    - The **Value** = **Data**
    - The **Key = Hash of the Data**
- You can use the key to retrieve the content

**The Key - SHA1**

- A cryptographic hash function
- Given a piece of data, it produces a 40-digit hexadecimal number
- This value should always be the same if the given input is the same

**The Value - BLOB**

- git stores the *compressed* data in a blob, along with metadata in header:
    - The identifier **blob**
    - the size of the content
    - \0 delimiter
    - content
- Where are the blobs stored
    - it is stored in our .git directory under the objects folder
- Blog needs more
    - It is missing filenames and directory structures!
    - Git stores this information in a **tree**
        - A tree contains pointers (using SHA1)
            - to blobs
            - to other trees
        - and metadata:
            - **type** of pointer (**blob** or **tree**)
            - **filename** or directory name
            - **mode** (executable file, symbolic link, ..)

    **Trees basically points to blobs & other trees**

    **Identical Content is Only Stored ONCE!**

    - Critical feature, saves space
    - If there is a identical copy, the copies will refer to the original SHA1