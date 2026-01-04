from PIL import Image
import numpy as np

# Load the original image
img = Image.open("/mnt/data/3DF45536-0178-43C7-99C6-A20D2834250D.jpeg").convert("RGBA")

# Convert to numpy for background replacement
data = np.array(img)
# All nearly-black pixels will be replaced with white
# Tune the threshold as needed
threshold = 40
r, g, b, a = data[:,:,0], data[:,:,1], data[:,:,2], data[:,:,3]
mask = (r < threshold) & (g < threshold) & (b < threshold)
data[:,:,:3][mask] = [255,255,255]

# Convert back to image
img_white_bg = Image.fromarray(data)
output_path = "/mnt/data/software_symbiose_whitebg.png"
img_white_bg.save(output_path)

output_path
