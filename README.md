# prebuilt-debug-jdk
Prebuilt openjdk images with debug and asan enabled

Example usage in a github workflow using [`addnab/docker-run-action`](https://github.com/addnab/docker-run-action):
```yml
- name: Run tests with address sanitizer
  uses: addnab/docker-run-action@v3
  with:
    registry: gcr.io
    image: ghcr.io/markusjx/prebuilt-debug-jdk:17-bullseye
    options: -v ${{ github.workspace }}:/app
    run: |
      # Build steps here
```

If there are errors about asan symbols not being found, simply point the `LD_PRELOAD`
environment variable to the appropriate file:
```sh
export LD_PRELOAD=$(clang -print-file-name=libclang_rt.asan-x86_64.so)
```