# NPM

## Resolving EACCES permissions errors when installing packages globally

1.  On the command line, in your home directory, create a directory for global installations:

    ```
     mkdir ~/.npm-global
    ```

2.  Configure npm to use the new directory path:

    ```
     npm config set prefix '~/.npm-global'
    ```

3.  In your preferred text editor, open or create a `~/.profile` file and add this line:

    ```
     export PATH=~/.npm-global/bin:$PATH
    ```

4.  On the command line, update your system variables:

    ```
     source ~/.profile
    ```

5.  To test your new configuration, install a package globally without using `sudo`:

    ```
     npm install -g jshint
    ```
