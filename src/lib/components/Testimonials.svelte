<script lang="ts">
	import { onMount } from 'svelte';

	const testimonials = [
		{
			text: 'HDM Sigorta ile kasko poliçemi yeniledim, aynı teminatla %30 daha uygun fiyat aldım. Danışmanım her aşamada yanımdaydı.',
			name: 'Ahmet Yılmaz',
			title: 'İşletme Sahibi'
		},
		{
			text: 'Sağlık sigortası konusunda çok detaylı bilgi aldım. 3 farklı şirketin teklifini karşılaştırıp en uygununu seçmeme yardımcı oldular.',
			name: 'Elif Kaya',
			title: 'Avukat'
		},
		{
			text: 'Konut sigortamda hasar yaşadığımda süreç çok hızlı ilerledi. Hasar departmanı gerçekten 7/24 destek veriyor.',
			name: 'Mehmet Demir',
			title: 'Mimar'
		},
		{
			text: 'Kurumsal sigorta ihtiyaçlarımız için yıllardır HDM Sigorta ile çalışıyoruz. Profesyonel ve güvenilir bir ekip.',
			name: 'Ayşe Öztürk',
			title: 'Finans Direktörü'
		},
		{
			text: 'Trafik sigortamı en uygun fiyata yaptırdım. Online teklif aldıktan 10 dakika içinde poliçem elimdeydi.',
			name: 'Can Arslan',
			title: 'Yazılım Mühendisi'
		},
		{
			text: 'Seyahat sigortası için son dakika başvuru yaptım, aynı gün içinde poliçemi ilettiler. Harika bir hizmet!',
			name: 'Zeynep Çelik',
			title: 'Öğretim Görevlisi'
		}
	];

	let swiperEl: HTMLElement;

	onMount(async () => {
		const { Swiper } = await import('swiper');
		const { Pagination, Autoplay } = await import('swiper/modules');
		await import('swiper/css');
		await import('swiper/css/pagination');

		new Swiper(swiperEl as any, {
			modules: [Pagination, Autoplay],
			slidesPerView: 1,
			spaceBetween: 24,
			autoplay: {
				delay: 5000,
				disableOnInteraction: true
			},
			pagination: {
				el: '.swiper-pagination',
				clickable: true
			},
			breakpoints: {
				768: { slidesPerView: 2 },
				1024: { slidesPerView: 3 }
			}
		});
	});

	function renderStars() {
		return Array(5).fill(0);
	}
</script>

<section id="yorumlar" class="py-20 lg:py-28 bg-teal-50">
	<div class="max-w-7xl mx-auto px-6">
		<div class="text-center mb-16" data-aos="fade-up">
			<span class="inline-block text-sm font-semibold text-teal-700 bg-teal-100 px-4 py-1.5 rounded-full mb-4">MÜŞTERİ YORUMLARI</span>
			<h2 class="font-heading font-bold text-3xl sm:text-4xl lg:text-[40px] text-charcoal-800 mb-4">
				Müşterilerimiz Ne Diyor?
			</h2>
			<p class="text-charcoal-500 max-w-2xl mx-auto text-lg">
				Binlerce mutlu müşterimizin deneyimlerini dinleyin.
			</p>
		</div>

		<div bind:this={swiperEl} class="swiper" data-aos="fade-up" data-aos-delay="100">
			<div class="swiper-wrapper pb-12">
				{#each testimonials as testimonial}
					<div class="swiper-slide">
						<div class="bg-white rounded-2xl p-8 shadow-sm h-full flex flex-col">
							<!-- Stars -->
							<div class="flex gap-1 mb-4">
								{#each renderStars() as _}
									<svg class="w-5 h-5 text-gold-500" fill="currentColor" viewBox="0 0 24 24"><path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/></svg>
								{/each}
							</div>

							<!-- Quote -->
							<p class="text-charcoal-600 leading-relaxed flex-1 mb-6">"{testimonial.text}"</p>

							<!-- Divider -->
							<div class="border-t border-charcoal-100 pt-4">
								<div class="font-heading font-semibold text-charcoal-800">{testimonial.name}</div>
								<div class="text-sm text-charcoal-500">{testimonial.title}</div>
							</div>
						</div>
					</div>
				{/each}
			</div>
			<div class="swiper-pagination"></div>
		</div>
	</div>
</section>
