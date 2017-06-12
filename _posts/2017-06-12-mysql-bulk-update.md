---
layout: post
title: "MySQL批量更新某个字段"
comments: true
keywords: ""
author: '丁'
---

#### 业务场景

在日常的业务开发过程中,我们通常会遇到需要批量更新一部分数据的某个字段的需求,比如批量排序. 如下图:

![mahua](http://7xp1dj.com1.z0.glb.clouddn.com/1E7918B3-4B51-43CA-BCDD-00A6F48ACE15.png)

当我们点击排序按钮之后,常规的做法是提交表单然后后台逐条取值,使用for循环批量更新数据.OK,这没有问题,但是有更为优秀的方法来帮我们处理这个问题,使用 INSERT INTO 来代替 UPDATE ,这样我们之前可能需要20次甚至更多次的sql查询可以被优化成只需要一条,
具体代码如下:

```
    /**
	 * 重新排序
	 *
	 * @param array $data
	 *              $data = ['id' => '排序值', 'id' => '排序值' ...]
	 * @return bool
	 */
	public function resort($data)
	{
		if (empty($data) || !is_array($data) || !count($data)) {
			return false;
		}

        // 构建SQL语句
		$values = array();
		foreach ($data as $id => $score) {
			$values[] = '(' . implode(',', array($id, $score)) . ')';
		}

		$values = implode(',', $values);

		// 采用insert into进行单次批量更新
		$sql = 'INSERT INTO `table_name` (id, score) VALUES ' . $values . ' ON DUPLICATE KEY UPDATE score=values(score)';
		if ($this->query($sql)) {
			if ($this->affected_rows()) {
				$ids = array_keys($data);
				foreach ($ids as $id) {
				    // to do something
				}
			}
			return true;
		}

		return false;
	}
```

上面的$this->query() & $this->affected_rows() 替换为自己常用的sql查询封装.