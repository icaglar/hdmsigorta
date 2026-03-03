<script lang="ts">
	const features = [
		{
			title: 'Bağımsız Danışmanlık',
			desc: 'Tek bir şirkete bağlı değiliz. 12 farklı şirketten size en uygun teklifi buluyoruz.'
		},
		{
			title: '7/24 Hasar Destek',
			desc: 'Hasar anında yanınızdayız. Gece gündüz destek hattımız her zaman açık.'
		},
		{
			title: 'En Uygun Fiyat Garantisi',
			desc: 'Aynı teminat paketini daha uygun fiyata bulamazsınız, farkını iade ediyoruz.'
		},
		{
			title: '25+ Yıl Deneyim',
			desc: 'Çeyrek asırlık tecrübemizle doğru poliçeyi seçmenize yardımcı oluyoruz.'
		}
	];
</script>

<section id="hakkimizda" class="py-20 lg:py-28 bg-white">
	<div class="max-w-7xl mx-auto px-6">
		<div class="grid lg:grid-cols-2 gap-12 lg:gap-20 items-center">
			<!-- Left content -->
			<div data-aos="fade-right">
				<span class="inline-block text-sm font-semibold text-teal-700 bg-teal-50 px-4 py-1.5 rounded-full mb-4">HAKKIMIZDA</span>
				<h2 class="font-heading font-bold text-3xl sm:text-4xl lg:text-[40px] text-charcoal-800 mb-6">
					Neden <span class="text-gold-gradient">HDM Sigorta</span>?
				</h2>
				<p class="text-charcoal-500 text-lg leading-relaxed mb-8">
					2001 yılından bu yana Türkiye'nin dört bir yanındaki müşterilerimize bağımsız sigorta danışmanlığı hizmeti veriyoruz.
					Amacımız, her müşterimize özel ihtiyaç analizi yaparak en kapsamlı korumayı en uygun fiyatla sunmaktır.
				</p>

				<!-- Feature list -->
				<div class="space-y-5">
					{#each features as feature}
						<div class="flex gap-4">
							<div class="shrink-0 w-10 h-10 bg-teal-50 rounded-xl flex items-center justify-center mt-0.5">
								<svg class="w-5 h-5 text-teal-700" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2.5"><path d="M5 13l4 4L19 7"/></svg>
							</div>
							<div>
								<h4 class="font-heading font-semibold text-charcoal-800 mb-1">{feature.title}</h4>
								<p class="text-charcoal-500 text-sm leading-relaxed">{feature.desc}</p>
							</div>
						</div>
					{/each}
				</div>
			</div>

			<!-- Right visual -->
			<div class="relative" data-aos="fade-left">
				<!-- Main visual card -->
				<div class="bg-gradient-to-br from-teal-800 to-teal-900 rounded-3xl p-8 lg:p-12 text-white relative overflow-hidden">
					<!-- Pattern overlay -->
					<div class="absolute inset-0 opacity-5">
						<div class="absolute top-4 right-4 w-32 h-32 border-2 border-white rounded-full"></div>
						<div class="absolute bottom-4 left-4 w-24 h-24 border-2 border-white rounded-full"></div>
					</div>

					<div class="relative">
						<div class="text-6xl font-heading font-extrabold text-gold-400 mb-2">25+</div>
						<div class="text-xl font-heading font-semibold mb-6">Yıllık Sektör Deneyimi</div>
						<p class="text-white/70 leading-relaxed mb-8">
							Türkiye'nin önde gelen sigorta şirketleriyle güçlü iş birlikleri kurarak müşterilerimize en avantajlı poliçeleri sunuyoruz.
						</p>

						<div class="grid grid-cols-2 gap-6">
							<div>
								<div class="text-3xl font-heading font-bold text-gold-400">50K+</div>
								<div class="text-sm text-white/60">Mutlu Müşteri</div>
							</div>
							<div>
								<div class="text-3xl font-heading font-bold text-gold-400">100K+</div>
								<div class="text-sm text-white/60">Aktif Poliçe</div>
							</div>
							<div>
								<div class="text-3xl font-heading font-bold text-gold-400">%98</div>
								<div class="text-sm text-white/60">Müşteri Memnuniyeti</div>
							</div>
							<div>
								<div class="text-3xl font-heading font-bold text-gold-400">12</div>
								<div class="text-sm text-white/60">Sigorta Şirketi</div>
							</div>
						</div>
					</div>
				</div>

				<!-- Floating glassmorphism card -->
				<div class="absolute -bottom-6 -left-6 glass rounded-2xl p-5 shadow-xl max-w-[220px]">
					<div class="flex items-center gap-3 mb-2">
						<div class="w-10 h-10 bg-teal-500 rounded-full flex items-center justify-center">
							<svg class="w-5 h-5 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"><path d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z"/></svg>
						</div>
						<div>
							<div class="text-sm font-semibold text-charcoal-800">Güvenli</div>
							<div class="text-xs text-charcoal-500">SEDDK Lisanslı</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</section>
