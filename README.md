<div align="center">

# Greefy

**Greefy** is a machine learning platform designed to efficiently create video game montages. It utilizes neural networks to detect highlights within video game footage.

[![Tech Stack](https://skillicons.dev/icons?i=python,svelte,ts,css,html,docker,bash,mongo,github)](https://skillicons.dev)

</div>



# Supported Games

Greefy currently supports the following games:

- **[Valorant](https://playvalorant.com/)**
- **[League of Legends](https://www.leagueoflegends.com/)**
- **[Overwatch 2](https://playoverwatch.com/)**
- **[CSGO 2](https://www.counter-strike.net/cs2)**
- **[The Finals](https://www.reachthefinals.com/)**

# Usage


## Setup

1. **Install Dependencies**

   - Install [FFmpeg](https://ffmpeg.org/about.html). Ensure that both `ffmpeg` and `ffprobe` are installed and added to your system's PATH.

2. **Run the Setup**

   - Unzip the downloaded release.
   - Run the appropriate setup script:
     - For Windows: `setup.bat`
    

3. **Add your Videos and Musics**

   - Place your video files (`.mp4` format) and audio files (`.mp3` format) into the `resources` folder.

### Python version

Currently, Greefy supports Python 3.8, 3.9, and 3.10.

## Configuration

Customize the application by editing the `settings.json` file. This is where you can adjust algorithm settings and select the game you are processing.

### Configuration Example

```json
{
  "neural-network": {
    "confidence": 0.8
  },
  "clip": {
    "framerate": 8,
    "second-before": 3,
    "second-after": 3,
    "second-between-kills": 5
  },
  "stretch": false,
  "game": "valorant"
}
```

### Available Settings

- **neural-network**
  - **confidence**: The confidence threshold used by the neural network. Lower values may include more frames but might introduce false positives.
- **clip**
  - **framerate**: The framerate at which the neural network processes the clips. Higher values include more frames but increase processing time.
  - **second-before**: Number of seconds to include before the highlight.
  - **second-after**: Number of seconds to include after the highlight.
  - **second-between-kills**: Maximum time between kills to be considered part of the same highlight. If the time between two highlights is less than this value, they will be merged.
- **stretch**: Set to `true` if you're playing on a 4:3 resolution but your clips are recorded in 16:9.
- **game**: The game you are processing. Options are `"valorant"`, `"overwatch"`, `"csgo2"`, `"the-finals"`, `"league-of-legends"`.

### Recommended Settings

It's recommended to experiment with the settings to achieve the best results for your videos. Below are some configurations that have worked well:

#### Valorant

```json
{
  "neural-network": {
    "confidence": 0.8
  },
  "clip": {
    "framerate": 8,
    "second-before": 4,
    "second-after": 0.5,
    "second-between-kills": 3
  },
  "stretch": false,
  "game": "valorant"
}
```

#### Overwatch 2

```json
{
  "neural-network": {
    "confidence": 0.6
  },
  "clip": {
    "framerate": 8,
    "second-before": 4,
    "second-after": 3,
    "second-between-kills": 5
  },
  "stretch": false,
  "game": "overwatch"
}
```

#### CSGO 2

```json
{
  "neural-network": {
    "confidence": 0.7
  },
  "clip": {
    "framerate": 8,
    "second-before": 4,
    "second-after": 1,
    "second-between-kills": 3
  },
  "stretch": false,
  "game": "csgo2"
}
```

#### The Finals

Since **The Finals** does not use the neural network, the settings differ slightly. The application uses image recognition and Optical Character Recognition (OCR) to detect kills. Due to the computational demands of OCR, processing can be slow.

**Recommendation:** Use a framerate of 4 to balance speed and accuracy. Increasing the framerate may improve results but will significantly increase processing time (a maximum of 8 is suggested).

```json
{
  "clip": {
    "framerate": 4,
    "second-before": 6,
    "second-after": 0,
    "second-between-kills": 6
  },
  "stretch": false,
  "game": "the-finals"
}
```

#### League of Legends

For **League of Legends**, image recognition is used to detect kills. A lower framerate is sufficient because kill indicators remain on the screen for an extended period.

```json
{
  "clip": {
    "framerate": 4,
    "second-before": 8,
    "second-after": 0,
    "second-between-kills": 10
  },
  "stretch": false,
  "game": "league-of-legends"
}
```

## Running the Application

After configuration, run the application using the appropriate script:

- For Windows: `run.bat`


# Frontend Overview

The frontend is a web application that allows you to interact with the Greefy algorithm and customize your video montages. It consists of five main sections:

1. **Clips**
2. **Segments**
3. **Music**
4. **Effects**
5. **Result**

## Clips

In the **Clips** section, you can:

- **View and manage your video clips**: See a list of your uploaded videos.
- **Rearrange clips**: Drag and drop to reorder your clips.
- **Select clips for segmentation**: Use the "Show" toggle to select which videos to process.
- **Add custom effects**: Apply effects to individual clips.
- **Generate segments**: After making your selections, click on **Generate Segments** to create highlights.

## Segments

In the **Segments** section, you can:

- **View generated segments**: See the list of highlights extracted by the algorithm.
- **Include or exclude segments**: Use the "Hide" toggle to exclude segments from the final montage.

## Music

In the **Music** section, you can:

- **Manage your music tracks**: View the list of music files added to the `resources` folder.
- **Select music for the montage**: Use the "Hide" toggle to exclude tracks.
- **Rearrange music**: Drag and drop to set the order of music tracks in your montage.

## Effects

In the **Effects** section, you can:

- **Apply global effects**: Add effects that will be applied to the entire video.
- **Override with clip effects**: Note that effects applied to individual clips will override these global effects.
- **Available effects**:
  - Blur
  - Horizontal Flip (`hflip`)
  - Vertical Flip (`vflip`)
  - Brightness
  - Saturation
  - Zoom
  - Grayscale

## Result

In the **Result** section, you can:

- **Preview your montage**: See the final assembled video with all clips, music, and effects applied.



### Q: How can I change the game ?

**A:** To change the game setting in Greefy, follow these steps:

1. **Stop the application.**
2. **Delete the `.data` folder and the `session` folder** in the Greefy directory.
3. **Edit `settings.json`** to specify the new game under the `"game"` key.
4. **Add and remove any necessary files in the resources folder** (e.g., new game dataset).
5. **Restart the application.**

These steps will reset the game configuration, and the new game will be applied upon starting Greefy.

