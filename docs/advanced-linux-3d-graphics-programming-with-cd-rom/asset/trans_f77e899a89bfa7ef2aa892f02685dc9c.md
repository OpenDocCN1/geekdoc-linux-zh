

0 = texture->O_original;
U = texture->U_original - 0;
V = texture->V_original - 0;

l3d_real min_u, minv, maxu;
int i = 0;

l3d_point tex_point;
tex_point =
    world_to_tex_matrix(*texture)
	| (*vlist) [(**ivertices)[i].i_vertex].original;
u = tex_point.X_ = l3d_divrr(tex_point.X_, tex_point.W_);
v = tex_point.Y_ = l3d_divrr(tex_point.Y_, tex_point.W_);
maxu = min_u = tex_point.X_;
maxv = minv = tex_point.Y_;
U = texture->U_original - texture->O_original;
V = texture->V_original - texture->O_original;

#define VTX(i) (((*vlist)[ (*clip_vvertices)[i].i_vertex ]),transformed)
for(i=1; i < ivertices->num_items; i++) {
	l3d_real u,v;
	
	tex_point =
	    world_to_tex_matrix(*texture)
		| (*vlist) [(**ivertices)[i].i_vertex].original;
	u = tex_point.X_ = l3d_divrr(tex_point.X_, tex_point.W_);
	v = tex_point.Y_ = l3d_divrr(tex_point.Y_, tex_point.W_);
	if(u<minu) minu=u;
	if(u>maxu) maxu=u;
	if(v<minv) minv=v;
	if(v>maxv) maxv=v;
	}
int iminu, iminv, imaxu, imaxv;

iminu = ifloor(minu);
iminv = ifloor(minv);
imaxu = iceil(maxu);
imaxv = iceil(maxv);

int u_tilecount = imaxu - iminu;
int v_tilecount = imaxv - iminv;

int u_tilecount_pow2 = 1<< iceil(float_to_l3d_real(log(u_tilecount) / log(2)));
int v_tilecount_pow2 = 1<< iceil(float_to_l3d_real(log(v_tilecount) / log(2)));
imaxu += v_tilecount_pow2 - u_tilecount;
imaxv += v_tilecount_pow2 - v_tilecount;

surface_xsize = texture->tex_data->width * (imaxu - iminu);
surface_ysize = texture->tex_data->height * (imaxv - iminv);

surface_orientation_0.original.set(0, X + U.X *minu + V.X *minv,
0, Y + U.Y *minu + V.Y *minv,
0, Z + U.Z *minu + V.Z *minv,
int_to_l3d_real (1));
surface_orientation_0.original.set(0, X + U.X *maxu + V.X *minv,
0, Y + U.Y *maxu + V.Y *minv,
0, Z + U.Z *maxu + V.Z *minv,
int_to_l3d_real (1));
surface_orientation_0.original.set(0, X + U.X *minu + V.X *maxv,
0, Y + U.Y *minu + V.Y *maxv,
0, Z + U.Z *minu + V.Z *maxv,
int_to_l3d_real (1));

assign_tex_coords_from_tex_space (surface_orientation);

void l3d_polygon_3d_textured_lightmapped::init_transformed (void) {
l3d_polygon_3d_textured ::init_transformed();

surface_orientation_0.transformed = surface_orientation_0.original;
surface_orientation_U.transformed = surface_orientation_U.original;
surface_orientation_V.transformed = surface_orientation_V.original;
}

void l3d_polygon_3d_textured_lightmapped::transform (const l3d_matrix &m, int count) {
l3d_polygon_3d_textured::transform(m,count);

surface_orientation_0.transformed = m * surface_orientation_0.transformed;
surface_orientation_U.transformed = m * surface_orientation_U.transformed;
surface_orientation_V.transformed = m * surface_orientation_V.transformed;
}

l3d_polygon_2d& l3d_polygon_3d_textured_lightmapped::clone (void) {
return new l3d_polygon_3d_textured_lightmapped (*this);
}

l3d_polygon_3d_textured_lightmapped::l3d_polygon_3d_textured_lightmapped
(const l3d_polygon_3d_textured_lightmapped &r)
: l3d_polygon_2d (r),
l3d_polygon_3d(r),
l3d_polygon_3d_textured (r),
l3d_polygon_3d_clipable(r),
l3d_texture_computer(r)
{
sCache = r.scache;
surface = r.surface;
surface_orientation = r.surface_orientation;
surface_xsize = r.surface_xsize;
surface_ysize = r.surface_ysize;
lightmap = r.lightmap;
}

成员变量 `scache` 是指向表面缓存的指针，该缓存负责管理多边形的表面。成员变量 `lightmap` 指向光照贴图，这是一个包含光照强度的小型纹理。成员变量 `surface` 指向表面本身，其中包含了平铺并经过光照处理的纹理版本。该表面由表面缓存创建，同时表面缓存也负责释放该表面。

## 146

第二章：3D 多边形渲染与动画技术

方法 `compute_surface_orientation_and_size` 根据原始纹理空间定义，确定多边形上原始纹理重复出现的次数。这是通过对多边形中的每个顶点应用世界空间到纹理空间的矩阵，并取生成的 u 和 v 值中的最大值和最小值来实现的。然后，由于纹理空间中距离为 1 表示纹理的一次重复，因此可以轻易通过最大值与最小值的差值计算出水平和垂直方向的重复次数。我们将水平和垂直的重复次数向上取整到 2 的整数次幂，然后分别乘以原始纹理的宽度和高度。我们将结果存储在 `surface_xsize` 和 `surface_ysize` 中。这些变量代表了预先平铺后的表面的总像素尺寸，该尺寸被方法 `combine_lightmap_and_texmap` 使用。

与所有纹理一样，表面的尺寸也是 2 的幂，因为这是原始软件光栅化器所要求的。

在计算出表面大小之后，我们还必须定义其朝向，并将其存储在成员变量 `surface_orientation` 中，这是一个纹理空间。我们通过按如下方式定义其纹理空间来定义表面的朝向。表面纹理空间的原点是原始纹理空间中多边形具有最小取整 (u,v) 值的位置。表面纹理空间 u 轴的尖端是原始纹理空间中具有最大取整 u 值和最

小取整 v 值的位置。表面纹理空间 v 轴的尖端是原始纹理空间中具有最小取整 u 值和最大取整 v 值的位置。换句话说，表面纹理空间的原点位于原始纹理空间中的整数坐标上。u 轴直接指向原始纹理空间中的 u 方向；v 轴直接指向 v 方向。u 和 v 轴的尖端也都精确地位于原始纹理空间中的整数坐标上。这种表面纹理空间的特殊整数对齐方式，加上表面包含整数而非分数个纹理重复次数的事实，意味着预先平铺的表面与原始纹理的相对位置是相同的——使用预先平铺的表面和新的表面朝向，其视觉效果与使用原始纹理和旧的纹理朝向完全相同。

随着表面的新大小和朝向，我们还必须为多边形顶点分配新的纹理坐标。由于表面及其 u 和 v 轴比原始纹理更大，基于表面的纹理坐标将与基于原始纹理的纹理坐标不同（小于后者）。我们只需调用 `assign_tex_coords_from_tex_space`，并将新的表面朝向作为参数传入。

类 `l3d_polygon_3d_textured_lightmapped` 的其他成员是标准的，无需冗长的解释。`clone` 方法和拷贝构造函数提供了通过抽象指针复制多边形的功能。`transform` 和 `init_transformed` 方法已被扩展以变换光照贴图朝向。重写的 `draw` 方法使带有光照贴图的多边形通过要求光栅化器进行绘制来绘制自身。现在我们来看用于光栅化带有光照贴图多边形的方

法。首先，我们查看软件光照贴图映射，然后查看使用硬件加速的相同技术。令人惊讶的是，这是软件光栅化比硬件光栅化更简单的情况之一。

### 光照贴图的软件光栅化

由于表面缓存已经预先平铺并预先照亮了纹理，软件光栅化器几乎不需要任何更改即可支持光照贴图映射。类 `l3d_rasterizer_3d_sw_imp` 中的方法 `draw_polygon_textured_lightmapped` 处理带有光照贴图多边形的光栅化。

首先，我们必须能够访问预先照亮、预先平铺的表面。如果成员变量 `surface` 中多边形的表面当前未分配（可能是因为多边形首次绘制，或者表面已创建但后来从缓存中丢弃），那么我们通过调用 `combine_lightmap_and_texmap`，使用预计算的表面宽度和高度来创建该表面。然后，我们将存储在多边形变量 `surface_orientation` 中的表面朝向分配给存储在表面内部的朝向。最后，我们简单地将多边形的 `texture` 成员变量分配为与新的 `surface` 变量相同，并使用现有的纹理映射例程绘制多边形。该表面已经预先平铺、预先照亮，并且朝向正确。因此，我们可以将其完全当作其他纹理处理，并像处理普通纹理映射多边形一样光栅化该多边形。

### 硬件光照贴图映射

在硬件加速的支持下，我们可以为光照贴图映射多边形使用另一种更直接的策略。由于 3D 硬件可以如此快速地光栅化多边形，因此我们对每个多边形进行两次遍历。首先，我们绘制具有纹理但未进行光照处理的多边形。然后，我们再次绘制相同的多边形，这次使用光照贴图，并且不替换现有的纹理像素，而是根据存储在光照贴图中的强度改变它们的强度。

![](img/a19d4e8b1d7eb6387691dc6c865430e6_163_0.png)

> 图 2.46：使用硬件时，我们在第一遍中绘制具有纹理但未应用光照贴图（左）的多边形。在此第一遍中，纹理贴图可以被平铺。在第二遍中，我们将光照贴图（中）应用到现有的纹理像素（右）上。光照贴图不被平铺。

这种双通道方法需要对我们的纹理映射策略进行三项主要修改：

- 我们不使用表面。换句话说，我们不将纹理和光照贴图合并为一个表面。因此，我们使用表面缓存分别存储纹理和光照贴图，而不是表面。
- 我们必须重新计算并重新分配多边形的纹理坐标以正确绘制纹理贴图，然后我们必须恢复原始纹理坐标，这些坐标最初在 `compute_surface_orientation_and_size` 中计算，定义了光照贴图的位置和朝向。
- 我们必须告知 Mesa 混合纹理贴图和光照贴图。

Mesa 光栅化器在例程 `draw_polygon_textured_lightmapped` 中绘制带有光照贴图的多边形。该例程首先在缓存中查找纹理数据，如果

