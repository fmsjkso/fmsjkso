- 👋 Hi, I’m @fmsjkso
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
fmsjkso/fmsjkso is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
$engine: 3
$onesync: on
name: VORPCore
author: vorpcore
description: VorpCore Official txAdmin recipe! This will set up a base vorp official server.

variables:
    steam_webApiKey: "none"

tasks:
# Recipe Specific server.cfg files
  - action: download_github
    src: https://github.com/VORPCORE/VORP_txAdmin
    ref: main
    dest: ./temp/vorp_txAdminRecipe
  
  - action: move_path
    src: ./temp/vorp_txAdminRecipe/server.cfg
    dest: ./server.cfg
  
# Run Database SQL
  - action: connect_database
  - action: query_database
    file: ./temp/vorp_txAdminRecipe/MariaDB.sql
    
# Download default CFX resources
  - action: download_github
    src: https://github.com/citizenfx/cfx-server-data
    ref: master
    subpath: resources
    dest: ./resources/

# Download Pre-Made Files
  - action: download_github
    src: https://github.com/VORPCORE/vorp_pre-made
    ref: main
    dest: ./temp/premade
  
# Move all vorp resources and files to root for txadmin
  - action: move_path
    src: ./temp/premade/server/resources/[VORP]
    dest: ./resources/[VORP]

  - action: move_path
    src: ./temp/premade/server/icon.png
    dest: ./icon.png

# Clean up temporary files
  - action: remove_path
    path: ./temp
