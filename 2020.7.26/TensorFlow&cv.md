#TensorFlow使用流程
##1、定义输入与输出
###在我们训练模型时以路径为输入得到图片，我们可以使用tf.placeholder定义数据类型
    image_path_placeholder = tf.placeholder(tf.string)

##2、定义数据之间的关系，即模型结构
###可以使用这些库
####slim
####tensorLayer
####keras

##3、定义损失函数
####定义损失函数以及训练方式
    cost=my_loss(prediction,truth)
    train_step = tf.train.AdamOptimizer(learning_rate=learing_rate).minimize(cost, global_step=global_steps)

##4、训练
####向前传播得到误差
    loss, summary_string, lr = sess.run([cost, merged_summary_op, learing_rate])      
####向后传播更新参数
    sess.run(train_step)

##5、预测
    result=model(input)
    r=sess.run(result)

##6保存与恢复
    ckpt_saver = tf.train.Saver(hed_weights, max_to_keep=cktp_max_num)
###保存
    ckpt_saver.save(sess, hed_ckpt_file_path, global_step=step)
###恢复
    latest_ck_file = tf.train.latest_checkpoint(checkpoint_dir)
    ckpt_saver.restore(sess, latest_ck_file)

#一些简单cv算法
    # 对gt膨胀一下 5次
    kernel = cv2.getStructuringElement(cv2.MORPH_ELLIPSE, (5, 5))
    dilate_gt = cv2.dilate(gt, kernel, iterations=5)
     
    # image alpha融合
    b_roi[:, :, :] = f_roi[:, :, :] * f_roi_weight[:, :, :] + b_roi[:, :, :] * (1 - f_roi_weight[:, :, :])
    
    
    #亮度gamma调整
    from skimage import exposure
    f_roi = exposure.adjust_gamma(f_roi, gamma)
    
    #随机修改亮度与对比度
    contrast = random.uniform(0.7, 1.5)
    brightness = random.uniform(-30, 30)
    img_out = np.uint8(np.clip((img_out * contrast + brightness), 0, 255))