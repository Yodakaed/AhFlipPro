

on:
  push:
    branches:
      - '**'
  pull_request:
  workflow_dispatch:
jobs:
  build:
    name: Build
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - name: Set up JDK 1.8
        uses: actions/setup-java@v1
        with:
          java-version: 1.8
      - name: Grant execute permission for gradlew
        run: chmod +x gradlew
      - name: Setup ForgeGradle
        run: ./gradlew setupCIWorkspace
      - name: Build with Gradle
        run: ./gradlew build
      - name: Upload Artifact
        uses: actions/upload-artifact@v2
        with:
          name: NotEnoughCoins
          path: "build/libs/*.jar"
          
