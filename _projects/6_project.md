---
layout: page
title: CS.93000
description: (2022, 1st Year Summer, KAIST) Immersion Camp - Collaborative Music Composition Website
img: assets/img/project/music.png
redirect: https://github.com/JinA0218/Mad-Music-Maker
importance: 6
category: coursework
---

# Collaborative Music Composition Website [[code]](https://github.com/JinA0218/Mad-Music-Maker) 

## 1. Developers

- Huh Hoejun: Korea University, Computer Science (entered in 2017)  
- Kim Sunghyuk: KAIST, Computer Science (entered in 2018)  
- Jina Kim: KAIST, School of Freshman (entered in 2022)

## 2. Development Environment

**Client**  
- React.js  

**Server**  
- Built with Node.js and Rust  
- Database: MySQL  

## 3. Application Overview

This is a simple web application that allows users to compose and upload music collaboratively.

### 1) Website Structure

- **Sign Up / Log In**  

  ![1](https://user-images.githubusercontent.com/80519883/185916951-1823044d-0ab1-404a-99bb-36c47babdb48.png)

- **SongMaker / My Music**  

  ![2](https://user-images.githubusercontent.com/80519883/185917015-56cf3f06-22d0-4b7e-9efd-fc8db6149592.png)

  - Clicking **SongMaker** opens a new composition window.  
  - Clicking **My Music** shows a list of all previously composed tracks.  

    ![3](https://user-images.githubusercontent.com/80519883/185917287-32781798-e7ef-4583-b216-780c5ea3ca51.png)  

    Each track includes the assigned **Name** and a **WAV file download link**. Users can click the link to play the composed music.  

---

### 2) SongMaker

#### (1) Main Screen

![6](https://user-images.githubusercontent.com/80519883/185917271-83b3af5e-9104-498c-8853-4a42335ce33a.png)

Users can set **Name (title), Tempo, and Rhythm**.  

Available buttons:  
- **+ Button**: Opens the composition window. Each + corresponds to an instrument, and additional instruments can be added.  
- **Play Test**: Generates and downloads a WAV file that plays the composed track.  
- **Upload**: Uploads the WAV file to **My Page**.  
- **My Page**: Displays the list of previously composed music.  

#### (2) Composition Screen

![4](https://user-images.githubusercontent.com/80519883/185917201-19a18d9a-489e-4f58-93d4-e90a080e645d.png)

1. **Basic Settings**  
   - **Note Length**: Defines note duration (number of vertical grid cells). Default = 1.  
   - **Note Type**: Instrument type. Available options: `sine, square, triangle, saw, synth1, synth2, kick, snare` (8 total).  

2. **Piano Roll**  
   - Horizontal axis = time, vertical axis = pitch.  
   - Default size: 32 cells (2 measures).  
   - Range: C4 (middle C) to C6.  
   - Clicking a cell places a note of the chosen length; clicking again removes it.  

3. **Score (Notation)**  
   - Generates sheet music using **ABC notation** (A–G representation).  

4. **Controls**  
   - **← Button**: Returns to the previous screen and adds the score to the workspace.  
   - **+ Button (top-right)**: Extends piano roll length by 16 cells, allowing longer compositions.  

By repeating these steps, users can complete a composition and view the score by instrument:  

![5](https://user-images.githubusercontent.com/80519883/185917313-3715dd34-e0f4-461f-8e4e-25aa072a1eb6.png)

---

### 3) Audio Generation

The server converts score data into audio files.  

1. Generates a **WAV file** and writes header information.  
2. Processes each note based on pitch and selected instrument, using appropriate waveform functions.  
3. Combines and outputs the final WAV file back to the client.  