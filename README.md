# #include<stdio.h>
#define max 3

struct slist
{
	int data[max];//这里我们可以用‘宏’来指定大小，或者用malloc来给他分配空间
	int length;
};

void init(struct slist* p)//把a的地址传给形参p
{
	//通过p,使顺序表变成空表
	p->length = 0;
}

void printlist( const struct slist* p)
{
	for (int i = 0; i < p->length; i++)
		printf("%d ", p->data[i]);
	putchar('\n');
}

int insert(struct slist* p, int k, int x)
{
	if (k<0 || k>p->length||p->length==max)//插入前需考虑失败情况              //这里很多人会写max-1;应该换成max;即表插入满后为max
		//1.插入位置不合法，不在指定范围内
		//范围：k---length-1
	
		//2.当前线性表已满
		//max-1:表示此时位置已满
		return 0;//插入失败
	else
	{
		for (int i = p->length - 1; i >= k; i--)
			//从最后的元素开始向往后移位
		{
			p->data[i + 1] = p->data[i];
		}
	}
	p->data[k] = x;//元素x被插入到第k个位置
	p->length++;//插入完后长度增加
	return 1;
}



int erase(struct slist* p, int k, int* px)
{
	if (k < 0 || k >= p->length)
		//失败条件
		//1.删除位置不合法
		//2.删除空表
		return 0;
	else
	{
		*px = p->data[k];//先把要删除的元素放入*px
		for (int i = k + 1; i < p->length; i++)//之后从k+1项开始往前挪
		{
			p->data[i - 1] = p->data[i];//元素往前开始移位
		}
		p->length--;//删除后长度减小
		return 1;

	}

}
int main(int argc, const char* argv[])
{
	struct slist a;
	//a.length = 0;      这里是初始化结构体
	//我们一般使用函数进行初始化
	int k = 0;
	int x = 0;
	init(&a);
	insert(&a, 0, 11);
	insert(&a, 0, 22);
	insert(&a, 1, 33);
	printlist(&a);//打印该表 
	erase(&a, 1, &x);

	printlist(&a);//打印该表 
	//关于传参为什么传地址
	//如果参数传a,a是一个结构体变量，它里面包含一个数组和整形length,传a的话它会把整个变量的值拷贝传进去
	//比较低效
	return 0;
}
