<?php

/**
 * Class Penci_Check_Envato_Code
 *
 * PHP’s cURL : http://marketplace.envato.com/api/edge/[USERNAME]/[API-KEY]/verify-purchase:[PURCHASE_KEY].json
 */
class Penci_Check_Envato_Code {

	protected $base_url = 'https:pencidesign.com/validate/';
	protected $username = '';  // Your Username
	protected $api_key = ''; // Set API Key

	public function __construct() {
		if ( get_option( 'penci_pennews_purchase_code' ) ) {
			return;
		}
		add_action( 'admin_menu', array( $this, 'add_page' ) );
		add_action( 'admin_notices', array( $this, 'validation_notice' ) );

		add_action( 'wp_ajax_penci_ajax_check_envato_code', array( $this, 'ajax_check_envato_code' ) );
		add_action( 'wp_ajax_nopriv_penci_ajax_check_envato_code', array( $this, 'ajax_check_envato_code' ) );

		add_action( 'edit_form_after_title', array( $this, 'box_active_theme' ) );
		add_action( 'admin_head', array( $this, 'enqueue_style' ) );
		add_action( 'init', array( $this, 'remove_post_type_support' ), 10 );

	}

	/**
	 * Add options page
	 */
	public function add_page() {
		add_menu_page(
			esc_html__( 'Active theme', 'pennews' ),
			esc_html__( 'Penci', 'pennews' ),
			'manage_options',
			'penci_theme',
			array( $this, 'admin_page' ),
			'',
			2
		);
	}

	/**
	 * Options page callback
	 */
	public function admin_page() {
		?>
		<div class="wrap">
			<h1><?php esc_html_e( 'Active theme', 'pennews' ); ?></h1>
			<div id="dashboard-widgets-wrap">
				<div id="dashboard-widgets" class="columns-2 metabox-holder">
					<div class="postbox-container">
						<div id="dashboard_right_now" class="postbox">

							<div class="main">
								<div class="penci-box penci-box-validation">
									<div class="penci-box-content">
										<div class="penci-validation">
											<h1 class="penci-validation-title"><?php esc_html_e( 'You are almost finished!', 'pennews' ); ?></h1>
											<p class="penci-validation-text">
												<?php esc_html_e( "Please activate PenNews to enjoy the full benefits of the theme.
												 We're sorry about this extra step but we built the activation system to prevent mass piracy of our themes, 
												 this allows us to better serve our paying customers.", 'pennews' ); ?>
											</p>
										</div>
										<span class="penci-status-text"></span>
										<div class="penci-validation-overlay">
											<div class="penci-validation-inner">
												<p class="penci-validation-text"></p>
												<a class="penci-btn penci-btn-lg penci-hide"></a>
											</div>
										</div>
									</div>
									<form id="penci-check-license" action="">
										<input class="penci-form-control" type="text" placeholder="<?php esc_html_e( 'Input Code and Hit Enter', 'pennews' ); ?>" value="">
									</form>
								</div>
							</div><!-- end main -->

						</div>
					</div>
				</div><!-- widget active theme -->
			</div>
		</div>
		<?php
		$this->add_js();
		$this->add_css();
	}

	/**
	 * Show notice active theme
	 */
	function validation_notice() {
		$screen = get_current_screen();

		// Don't show notice on page active theme
		if ( isset( $screen->parent_base ) && 'penci_theme' == $screen->parent_base ) {
			return;
		}

		$link_page_active = admin_url( 'admin.php?page=penci_theme' );
		?>
		<div class="notice notice-success is-dismissible">
			<p>
				<a class="penci-notice-logo" href="<?php echo esc_url( 'http://pencidesign.com/' ); ?>" target="_blank"><?php $this->get_icon_penci(); ?></a>
				<?php printf( __( ' This PenNews license is ​<strong>not validated</strong>​. <a href="%s">Fix</a>', 'pennews' ), esc_url( $link_page_active ) ); ?>
			</p>
		</div>
		<?php
	}

	/**
	 * Get icon penci
	 */
	function get_icon_penci() {
		?>
		<svg style="position: relative; top:4px;margin-right: 5px;" version="1.0" xmlns="http://www.w3.org/2000/svg"
		     width="18px" height="18px" viewBox="0 0 26.000000 26.000000"
		     preserveAspectRatio="xMidYMid meet">
			<g transform="translate(0.000000,26.000000) scale(0.100000,-0.100000)"
			   fill="#000000" stroke="none">
				<path d="M72 202 l-62 -60 0 -66 0 -66 125 0 125 0 0 61 0 61 -63 65 -62 64
				-63 -59z m73 28 c3 -5 -3 -10 -15 -10 -12 0 -18 5 -15 10 3 6 10 10 15 10 5 0
				12 -4 15 -10z m57 -57 c34 -33 36 -38 20 -49 -14 -10 -21 -8 -45 12 -36 31
				-62 30 -93 -1 -21 -21 -28 -23 -44 -13 -19 12 -18 14 17 50 51 52 92 52 145 1z
				m-77 -93 c0 -59 -1 -60 -27 -60 -26 0 -28 3 -28 42 0 24 7 49 17 60 28 32 38
				21 38 -42z m49 44 c10 -9 16 -33 16 -60 0 -40 -2 -44 -25 -44 -24 0 -25 3 -25
				60 0 62 7 71 34 44z m-130 -20 c9 -8 16 -31 16 -50 0 -27 -4 -34 -20 -34 -17
				0 -20 7 -20 50 0 28 2 50 4 50 3 0 12 -7 20 -16z m201 -34 c0 -44 -3 -50 -20
				-50 -18 0 -20 5 -17 38 4 35 17 62 31 62 3 0 6 -22 6 -50z"/>
				<path d="M90 70 c0 -5 5 -10 10 -10 6 0 10 5 10 10 0 6 -4 10 -10 10 -5 0 -10
				-4 -10 -10z"/>
			</g>
		</svg>
		<?php
	}

	/**
	 * Add js check license
	 */
	function add_js() {
		?>
		<script>
			var $checkLicense = jQuery( '#penci-check-license' ),
				$input = $checkLicense.find( '.penci-form-control' ),
				$validation = jQuery( '.penci-validation' ),
				$status = jQuery( '.penci-status-text' ),
				$overlay = jQuery( '.penci-validation-overlay' ),
				$button = jQuery( '.penci-validation-overlay .penci-btn' );

			$input.focus();

			$button.click( function () {
				$overlay.removeClass( 'penci-active' );
			} );

			$checkLicense.on( 'submit', function ( e ) {

				e.preventDefault();

				var inputVal = $input.val();


				if ( ! inputVal ) {
					return false;
				}


				var ajaxUrl = '<?php echo admin_url( 'admin-ajax.php' ); ?>';
				var nonce = '<?php echo wp_create_nonce( 'ajax-nonce' ) ?>';
				$input.prop( 'disabled', true );

				$status.html( 'Verifying license…' );
				$validation.addClass( 'penci-processing' );
				$overlay.removeClass( 'penci-active' );
				jQuery( '.penci-btn' ).removeClass( 'penci-hide' );

				var data = {
					action: 'penci_ajax_check_envato_code',
					envato_code: inputVal,
					nonce: nonce
				};

				jQuery.post( ajaxUrl, data, function ( response ) {
					$status.html( '' );
					$validation.removeClass( 'penci-processing' );

					if ( ! response.success ) {
						$input.prop( 'disabled', false );
						$button.html( response.data.button ).removeClass( 'penci-hide' );
					} else {
						$button.removeClass( 'penci-hide' );
					}

					$overlay.addClass( 'penci-active' );
					$overlay.find( '.penci-validation-text' ).html( response.data.message );

				} );

				return false;
			} );
		</script>
		<?php
	}

	/**
	 * Add css box active theme
	 */
	function add_css() {
		?>
		<style>
			.penci-box-validation {

			}

			.penci-validation {
				position: relative;
				padding: 5%;
				text-align: center;
				transition: opacity 0.65s cubic-bezier(0.23, 1, 0.32, 1), transform 0.65s cubic-bezier(0.23, 1, 0.32, 1);
			}

			.penci-validation.penci-processing {
				opacity: 0;
				transform: scale(0.85);
			}

			.penci-box-content {
				overflow: hidden;
				position: relative;
				padding: 1.5em;
				background-color: #fff;
				border-bottom: 1px solid rgba(0, 0, 0, 0.075);
				text-align: center;
			}

			.wrap h1.penci-validation-title {
				margin: .85714em auto;
				font-size: 1.5em;
				letter-spacing: -0.015em;
				color: currentColor;
			}

			p.penci-validation-text {
				max-width: 40em;
				margin-left: auto !important;
				margin-right: auto !important;
				line-height: 1.7;
				margin-bottom: 0;
			}

			.penci-validation.penci-processing + .penci-status-text {
				opacity: 1;
				transform: scale(1);
				pointer-events: auto;
			}

			.penci-status-text {
				display: block;
				overflow: hidden;
				position: absolute;
				top: 50%;
				left: 0;
				right: 0;
				margin: -0.5em auto 0;
				padding: 0 1.5em;
				font-size: 1.25em;
				font-weight: 600;
				line-height: 1.2;
				text-align: center;
				text-overflow: ellipsis;
				white-space: nowrap;
				pointer-events: none;
				opacity: 0;
				transform: scale(0.85);
				transition: opacity 0.65s cubic-bezier(0.23, 1, 0.32, 1), transform 0.65s cubic-bezier(0.23, 1, 0.32, 1);
			}

			.penci-validation-overlay {
				position: absolute;
				top: 0;
				left: 0;
				right: 0;
				bottom: 0;
				padding: 1.5em;
				text-align: center;
				color: #23282d;
				background-color: #fff;
				pointer-events: none;
				opacity: 0;
				transform: scale(1.15);
				transition: opacity 0.65s cubic-bezier(0.23, 1, 0.32, 1), transform 0.65s cubic-bezier(0.23, 1, 0.32, 1);
				z-index: 4;
				display: flex;
				justify-content: center;
				align-items: center;
			}

			.penci-validation-overlay.penci-active {
				pointer-events: auto;
				opacity: 1;
				transform: scale(1);
			}

			#penci-check-license input[type="text"] {
				border: 0;
				font-size: 2em !important;
				font-weight: 600;
				letter-spacing: -0.035em;
				text-align: center;
				border-radius: 0;
				-webkit-box-shadow: none;
				box-shadow: none;
				width: 100%;
				transition: margin 0.65s cubic-bezier(0.23, 1, 0.32, 1);
			}

			#penci-check-license input[type="text"]::-webkit-input-placeholder,
			#penci-check-license input[type="text"]::-moz-placeholder,
			#penci-check-license input[type="text"]::-ms-input-placeholder,
			#penci-check-license input[type="text"]::-webkit-input-placeholder {
				color: rgba(0, 0, 0, 0.25)
			}

			.penci-validation-overlay .penci-btn.penci-hide {
				display: none;
			}

			.penci-validation-overlay .penci-btn {
				background: #0085BA;
				border-color: #006799;
				box-shadow: 0px 1px 0px #006799;
				color: #fff;
				height: 44px;
				font-size: 18px;
				line-height: 40px;
				text-align: center;
				display: inline-block;
				text-decoration: none;
				margin: 15px 0 0;
				padding: 0 10px 1px;
				cursor: pointer;
				border-width: 1px;
				border-style: solid;
				-webkit-appearance: none;
				-webkit-border-radius: 3px;
				border-radius: 3px;
				white-space: nowrap;
				-webkit-box-sizing: border-box;
				-moz-box-sizing: border-box;
				box-sizing: border-box;
			}

			.penci-validation-overlay .penci-btn:hover {
				background: #008EC2;
				border-color: #006799;
				color: #fff;
			}

			@media screen and (min-width: 1050px) {
				.wrap h1.penci-validation-title {
					font-size: 2em;
				}
			}


		</style>
		<?php
	}

	/**
	 * Run ajax
	 *
	 * @return bool
	 */
	public function ajax_check_envato_code() {
		if ( ! isset( $_REQUEST['nonce'] ) ) {
			return false;
		}

		if ( ! wp_verify_nonce( $_POST['nonce'], 'ajax-nonce' ) ) {
			wp_send_json_error();
		}

		if ( ! current_user_can( 'manage_options' ) || ! isset( $_POST['envato_code'] ) || ! $_POST['envato_code'] ) {
			wp_send_json_error( array( 'message' => 'No purchase code specified.' ) );
		}


		$code = sanitize_text_field( $_POST['envato_code'] );

		//$request_url = 'https:pencidesign.com/validate/';
		//$uri = add_query_arg( array( 'envato_code'  => trailingslashit( $code ) ), $this->$base_url );
		//$request = wp_remote_get( $uri, array( 'timeout' => 15 ) );

		$purchase_data = $this->verify_envato_purchase_code( $code );
		$response      = $this->get_validation_response( $purchase_data );

		if ( isset( $purchase_data['verify-purchase']['buyer'] ) ) {
			$this->update_validation( $code );
		} else {
			$this->update_validation( '' );
			wp_send_json_error( $response );
		}


		wp_send_json_success( $response );
	}

	/**
	 * Show markup box active theme
	 */
	public function box_active_theme() {
		?>

		<div id="penci_toggle_notice">
			<div class="postbox penci_admin-push-top">
				<div class="penci_admin-section-title penci_admin-content">
					<div class="penci_admin-heading">
						<?php esc_html_e( 'You are almost finished!', 'pennews' ); ?>
					</div>
					<p class="penci_admin-excerpt">
						<?php esc_html_e( "Please activate PenNews to enjoy the full benefits of the theme.
							 We're sorry about this extra step but we built the activation system to prevent mass piracy of our themes, 
							 this allows us to better serve our paying customers.", 'pennews' ); ?>
					</p>
				</div>
				<div class="penci_admin-button-well clearfix">
					<a href="<?php echo admin_url( 'admin.php?page=penci_theme' ); ?>" class="button btn-massive btn-primary btn-full">
						<?php esc_html_e( 'Active theme', 'pennews' ); ?>
					</a>
				</div>
			</div>
		</div>
		<?php
	}

	/**
	 * Add style box after
	 */
	public function enqueue_style() {
		?>
		<style>
			.penci_admin-push-top {
				margin-top: 20px !important;
			}

			.penci_admin-content {
				padding: 20px;
				position: relative;
			}

			.penci_admin-section-title .penci_admin-heading {
				margin: 0;
				padding: 0;
				font-size: 28px;
				line-height: 38px;
				color: #222;
				font-weight: 400;
			}

			.penci_admin-section-title .penci_admin-excerpt {
				max-width: 830px;
				margin: 10px 0 0;
				padding: 0;
				font-size: 20px;
				line-height: 30px;
				color: #777;
			}

			.penci_admin-button-well {
				overflow: hidden;
				padding: 10px;
				clear: both;
				border-top: 1px solid #E5E5E5;
				background: #F5F5F5;
			}

			.penci_admin-button-well .button.btn-primary,
			.penci_admin-button-well .btn-primary {
				background: #0085BA;
				border-color: #006799;
				box-shadow: 0px 1px 0px #006799;
				color: #fff;
				height: 44px;
				font-size: 18px;
				line-height: 40px;
				display: block;
				text-align: center;
			}

			.penci_admin-button-well .button.btn-primary:hover,
			.penci_admin-button-well .btn-primary:hover {
				background: #008EC2;
				border-color: #006799;
				color: #fff;
			}
		</style>
		<?php
	}

	/**
	 * Hide editor,  thumbnail, post format when user isn't active theme
	 */
	public function remove_post_type_support() {
		remove_post_type_support( 'post', 'post-formats' );
		remove_post_type_support( 'post', 'editor' );
		remove_post_type_support( 'post', 'thumbnail' );
		remove_post_type_support( 'page', 'editor' );
		remove_post_type_support( 'page', 'thumbnail' );
	}


	public function get_validation_response( $purchase_data ) {

		if ( isset( $purchase_data['verify-purchase']['buyer'] ) ) {
			return array(
				'complete' => true,
				'message'  => __( '<strong>Congratulations,</strong> your site is now validated!', 'pennews' )
			);
		}

		// Purchase code is not valid
		return array(
			'message' => __( 'We&apos;ve checked the code, but it <strong>doesn&apos;t appear to be an PenNews purchase code or Penci license.</strong> Please double check the code and try again.', 'pennews' ),
			'button'  => __( 'Go Back', 'pennews' ),
		);

	}

	/**
	 * Update purchase code
	 *
	 * @param $code
	 */
	public function update_validation( $code ) {

		if ( $code ) {
			update_option( 'penci_pennews_purchase_code', $code );
		} else {
			delete_option( 'penci_pennews_purchase_code' );
		}
	}

	/**
	 * Verify envato purchase code
	 *
	 * @param $code
	 *
	 * @return array|mixed|object
	 */
	function verify_envato_purchase_code( $code ) {

		$username = $this->username;
		$api_key  = $this->api_key;

		// Open cURL channel
		$ch = curl_init();

		// Set cURL options
		curl_setopt( $ch, CURLOPT_URL, "http://marketplace.envato.com/api/edge/" . $username . "/" . $api_key . "/verify-purchase:" . $code . ".json" );
		curl_setopt( $ch, CURLOPT_RETURNTRANSFER, 1 );

		//Set the user agent
		$agent = 'Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1)';
		curl_setopt( $ch, CURLOPT_USERAGENT, $agent );
		// Decode returned JSON
		$output = json_decode( curl_exec( $ch ), true );

		// Close Channel
		curl_close( $ch );

		// Return output
		return $output;

	}

}

//new Penci_Check_Envato_Code;

