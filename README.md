# resize.pi
import os
from PIL import Image

input_folder = "input_images"          
output_folder = "output_images"      
target_size = (800, 600)               
output_format = "JPEG"                 
output_extension = ".jpg"           


def resize_and_convert_images():
    if not os.path.exists(output_folder):
        os.makedirs(output_folder)

    for filename in os.listdir(input_folder):
        filepath = os.path.join(input_folder, filename)
        try:
            with Image.open(filepath) as img:
                # Resize image
                img_resized = img.resize(target_size, Image.ANTIALIAS)

                # Convert and save
                base_filename = os.path.splitext(filename)[0]
                output_path = os.path.join(output_folder, base_filename + output_extension)
                img_resized.convert("RGB").save(output_path, output_format)

                print(f"Processed: {filename} -> {output_path}")
        except Exception as e:
            print(f"Failed to process {filename}: {e}")

if __name__ == "__main__":
    resize_and_convert_images()
