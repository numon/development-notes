## Custom audio tag

```jsx harmony

import React, { useCallback, useEffect, useRef, useState } from 'react';
import { makeStyles } from '@material-ui/core/styles';
import Grid from '@material-ui/core/Grid';
import Typography from '@material-ui/core/Typography';
import Slider from '@material-ui/core/Slider';
import VolumeDown from '@material-ui/icons/VolumeDown';
import VolumeUp from '@material-ui/icons/VolumeUp';
import Tooltip from '@material-ui/core/Tooltip';
import PauseCircleFilledOutlinedIcon from '@material-ui/icons/PauseCircleFilledOutlined';
import PlayArrowOutlinedIcon from '@material-ui/icons/PlayArrowOutlined';
import { useHistory } from 'react-router';
import { useDispatch } from 'react-redux';
import { formatValue } from '../../utils/handlers/data';


const useStyles = makeStyles({
  root: {
    width: 600,
    backgroundColor: 'rgba(255, 255, 255, 0.2)',
    borderRadius: '4px',
    marginRight: '1em',
  },
  playButton: {
    paddingLeft: '16px',
  },
  rightButton: {
    paddingRight: '16px',
  },
  gridContainer: {
    paddingTop: '6px',
  },
  title: {
    fontSize: 14,
    color: '#fff',
    paddingLeft: '16px',
  },
});

const valueToPercent = (currentTime, duration) => Math.round((currentTime / duration) * 100);

const AudioPlayer = ({ url, name }) => {
  const history = useHistory();
  const dispatch = useDispatch();
  const audio = useRef(null);
  const classes = useStyles();

  const [play, setPlay] = useState(true);
  const [volume, setVolume] = React.useState(100);
  const [duration, setDuration] = useState(0);
  const [currentTime, setCurrentTime] = useState(0);
  const currentTimeInterval = useRef(null);

  const playMusic = useCallback(() => {
    setPlay(true);
    audio.current.play();
    currentTimeInterval.current = setInterval(() => {
      setCurrentTime(audio.current.currentTime);
    }, 1000);
  }, [currentTimeInterval]);

  const stopMusic = useCallback(() => {
    setPlay(false);
    audio.current.pause();
    clearInterval(currentTimeInterval.current);
  }, [currentTimeInterval]);

  const handleChangeVolume = useCallback((event, newValue) => {
    setVolume(newValue);
    audio.current.volume = newValue / 100;
  }, []);

  const handleOnLoad = useCallback(() => {
    setCurrentTime(audio.current.currentTime);
    setDuration(audio.current.duration);
  }, []);

  const handleSliderChange = useCallback((e, newValue) => {
    audio.current.currentTime = (duration / 100) * newValue;
    setCurrentTime(Math.round(audio.current.currentTime));
  }, [duration]);

  function ValueLabelComponent(props) {
    const { children, open, value } = props;
    const curTime = formatValue((duration / 100) * value);
    return (
      <Tooltip open={open} enterTouchDelay={10} placement="top" title={curTime}>
        {children}
      </Tooltip>
    );
  }

  useEffect(() => {
    audio.current.load();
    playMusic();
    return () => clearInterval(currentTimeInterval.current);
  }, [currentTimeInterval, playMusic, url]);

  // call dispatch and remove podcast if change url
  history.listen(location => {
    if (location !== history.location.pathname) dispatch(PlayRemove());
  });

  return (
    <div className={classes.root}>
      <audio ref={audio} onLoadedMetadata={handleOnLoad}>
        <source
          src={url}
          type="audio/mpeg"
        />
        Your browser does not support the audio element.
      </ audio>
      <Grid container spacing={1} className={classes.gridContainer}>
        <Grid item xs={1}>
          {play
            ? <PauseCircleFilledOutlinedIcon
              onClick={stopMusic}
              className={classes.playButton}
            />
            : <PlayArrowOutlinedIcon
              onClick={playMusic}
              className={classes.playButton}
            />
          }
        </Grid>
        <Grid item xs={1}>
          <Typography gutterBottom>
            {formatValue(currentTime)}
          </Typography>
        </Grid>
        <Grid item xs={6}>
          <Slider
            value={valueToPercent(currentTime, duration)}
            defaultValue={0}
            aria-labelledby="continuous-slider"
            ValueLabelComponent={ValueLabelComponent}
            onChange={handleSliderChange}
            onMouseDown={stopMusic}
            onMouseUp={playMusic}
          />
        </Grid>
        <Grid item xs={1}>
          <Typography gutterBottom>
            {formatValue(duration)}
          </Typography>
        </Grid>
        <Grid item xs={3}>
          <Grid container spacing={1}>
            <Grid item>
              <VolumeDown/>
            </Grid>
            <Grid item xs>
              <Slider
                value={volume}
                onChange={handleChangeVolume}
                aria-labelledby="continuous-slider"
              />
            </Grid>
            <Grid item>
              <VolumeUp className={classes.rightButton}/>
            </Grid>
          </Grid>
        </Grid>
      </Grid>
      <Typography className={classes.title} color="textSecondary" gutterBottom>
        Podcast playing : <b>{name}</b>
      </Typography>
    </div>
  );
};

export default AudioPlayer;
