```
import cv2
from pathlib import Path

# Function to extract frames from a video

def extract_frames(video_file_path:Path,ouput_dir:Path) -> None:
    cap=cv2.VideoCapture(video_file_path)
    fps=int(cap.get(cv2.CAP_PROP_FPS))
    print(f'{fps = }')
    
    ouput_dir.mkdir(exist_ok=True)


    success, image = cap.read()
    frame_count=0

    while success:
        if frame_count % fps == 0:
            frame_time = frame_count // fps
            frame_filename = output_dir / f'frame_{frame_time}.jpg'
            cv2.imwrite(frame_filename,image)
            print(f'{frame_filename = }')

        success,image = cap.read()
        frame_count +=1


if __name__=='__main__':
    video_file=Path('video.mp4')
    output_dir=Path('frames')
    extract_frames(video_file_path=video_file,ouput_dir=output_dir)
```
