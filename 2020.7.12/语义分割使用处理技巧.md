对于目的种类的分割，我们可以先使用语义分割的结果图，找到对应像素再使用找边界函数这样可以达到较好的效果    # #只保留需要的类将其设置为255 其他为0

gt = cv2.cvtColor(gt, cv2.COLOR_BGR2GRAY)
gt_mask = (gt == cls)
gt = np.zeros_like(gt)
gt[gt_mask] = 255

gt[gt_mask] = gt[gt_mask]-1
gt_mask1 = (gt_mask & ~gt_mask)

# 对gt膨胀一下 5次
dilate_gt = gt.copy()
kernel = cv2.getStructuringElement(cv2.MORPH_ELLIPSE, (5, 5))
dilate_gt = cv2.dilate(dilate_gt, kernel, iterations=5)
# 得到膨胀后的手指mask roi区域
contours, _ = cv2.findContours(dilate_gt, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_NONE)