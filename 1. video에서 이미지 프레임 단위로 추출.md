# 📌 Video Frame Extractor

이 프로젝트는 OpenCV를 활용해 **동영상에서 일정 간격(초 단위)으로 프레임을 추출**하는 간단한 Python 스크립트입니다.  

---

## 🔧 기능 설명
- 입력된 동영상 파일(`video.mp4`)에서 FPS(Frame Per Second)를 계산합니다.
- FPS 단위로 프레임을 추출 → 즉, **1초에 1프레임** 저장합니다.
- 추출된 프레임은 지정된 디렉터리(`frames/`)에 `.jpg` 파일로 저장됩니다.
- 저장되는 프레임 이름은 `frame_{time_in_seconds}.jpg` 형식으로 관리됩니다.  

## 📂 프로젝트 구조
📦 video-frame-extractor

┣ 📜 extract_frames.py # 프레임 추출 코드

┣ 📜 video.mp4 # 테스트용 동영상 (예시)

┗ 📂 frames/ # 추출된 프레임이 저장될 폴더

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
